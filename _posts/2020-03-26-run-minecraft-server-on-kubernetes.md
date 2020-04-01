---
layout: post
title: "Run a Minecraft Bedrock Server on Kubernetes"
modified: 2020-03-26 16:30:10 +0000
tags: [kubernetes, minecraft, bedrock, googlecloud]
image:
  feature: feature/minecraft-bedrock-server.png
  credit: Casey West Jr
  creditlink: 
description: Run Minecraft Bedrock Server on Kubernetes reliably with persistent storage.
---

Do you, your kids, or your friends enjoy playing Minecraft on their Xbox, Windows PC, or mobile phones? If so this tutorial helps you get a Minecraft Bedrock server running reliabily on Kubernetes. Bedrock is the version which supports all platforms that aren't Java Edition[^0].

# Prerequisites

This quick guide uses [Google Cloud Platform] to spin up a small managed [Kubernetes] cluster on [GKE] to run a [Minecraft Bedrock Server]. I'm going to use [Cloud Shell] as my client which gives me the following prerequisites out of the box:

* The [gcloud] SDK.
* [kubectl] to interact with a Kubernetes cluster.

If you want to use GCP you can get started pretty quickly by cloning the gist repo with this handy link. I recommend opening it in a new tab.

[![Open in Cloud Shell](https://gstatic.com/cloudssh/images/open-btn.svg)](https://ssh.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://gist.github.com/884a95684acfa05b10c1c2545290f903.git)

# Create Your Cluster

This cluster has one node (virtual machine) to run your bedrock server. If you want to deploy multiple servers, for instance one for each of your children so they don't PvP in game or IRL, you might want to change this config a little to add more nodes or change the node size.

The most important choices you'll make here are node size and zone placement.

Node Size
: You can review all [GCE instance pricing] before committing. I'm choosing a server that, at the time of this writing, costs about $56USD/month.

Zone Placement
: It's recommended you choose a zone in a region that's close to you geographically. Take a look at our [locations] in the docs.

Also note the CPU and Memory resource requests. The machine I chose, `n2-standard-2`, has 8Gb of memory available. 

{% gist 884a95684acfa05b10c1c2545290f903 gke-cluster-creation.sh %}

# Deploy Minecraft Bedrock Server

Below is the configuration describing what you need to deploy the server. Let's break it down:

`StorageClass`
: I'm using SSDs because they're faster and the name of the game, other than Minecraft, is keeping latency low. They're more expensive, so you can leave this option out if you don't want it by removing the `storageClassName` in the `PersistentVolumeClaim` configuration. Note that I'm also enabling volume expansion so when we need more space. When you want to grow space available follow (this blog post)[PVC Expansion] to do it.

`PersistentVolumeClaim`
: We want server data like world generation, whitelisted users, and all the beautiful creations you've made to persist between restarts and upgrades. Here we're allocating a persistent volume for the cluster with a storage capacity of 1 Gig to start.
  
`Deployment`
: We're running one `replica`, or instance, of the server allocating 50% of the node's memory, and around half of its CPU to the Minecraft server. You can adjust that to your needs. Also take a look at the `env` entries. Mojang requires the end user, you, to accept the End User License Agreement and that's available through the `EULA` environment variable. You set the game mode between creative, survival, and hardcore; difficulty to peaceful, easy, normal, or hard; enforce Xbox Live accounts with `ONLINE_MODE`, and allow cheats like `/gamerule showcoordinates true` for operators. All the available settings are listed in the [docker container repo on GitHub][docker-minecraft-bedrock-server].

`Service`
: To expose this server online and make it possible for you to connect you need a service. We're using a `LoadBalancer` to make the server available on the typical port via UDP.

{% gist 884a95684acfa05b10c1c2545290f903 minecraft-bedrock-server.yaml %}

Apply this configuration to your cluster.

~~~sh
kubectl apply -f minecraft-bedrock-server.yaml
~~~

# Configure Your Player Whitelist

By enabling the White List in the server configuration above the server is locked down. No players can access it. Let's change that by allowing only the players you choose to join. You'll need the "Gamertag" (Xbox Live username) for each player you want to give access to. Write a JSON file like the following and add the players you want on your server.

{% gist 884a95684acfa05b10c1c2545290f903 whitelist.json %}

Now add the whitelist to the server. Copy the whitelist into the persistent volume claimed by the running server with the following command, then restart Minecraft.

~~~sh
kubectl cp whitelist.json \
  $(kubectl get pod -l app=mc-bedrock -o custom-columns=:metadata.name):/data/whitelist.json

kubectl rollout restart deployment/mc-bedrock
~~~

If you want to, you can watch the logs as the server starts up and you attempt to connect.

~~~sh
kubectl logs -f deployment/mc-bedrock
~~~

To connect, you'll need the IP address assigned to the `Service` which you can obtain by inspecting the service.

~~~sh
kubectl get service mc-bedrock -o jsonpath='{.status.loadBalancer.ingress[0].ip}'
~~~

# Give Operator Permissions

You may want to give one or more players operator status on the server. This will let them use special commands or whitelist new players in-game. That's done with another JSON file in the form shown here.

{% gist 884a95684acfa05b10c1c2545290f903 permissions.json %}

Your "XUID" is a the unique identifier for your Xbox Live account. The best way I've managed to find this, honestly, is to view the logs when whitelisted players connect to the server. To find the `XUID` run the following command.

~~~sh
kubectl logs deployment/mc-bedrock | grep xuid
~~~

Copy the `xuid` you find in the log entry into your `permissions.json` file, upload it to persistent storage, and restart the server one more time!

~~~sh
kubectl cp permissions.json \
  $(kubectl get pod -l app=mc-bedrock -o custom-columns=:metadata.name):/data/permissions.json

kubectl rollout restart deployment/mc-bedrock
~~~

# Backup and Restore

If you love yourself, your kids, or your friends enough you can implement `VolumeSnapshot`s for the `mc-bedrock` `PersistentVolumeClaim`. It's more or less straight forward. Here are some [docs](https://kubernetes.io/docs/concepts/storage/volume-snapshots/) and a [blog post](https://kubernetes.io/blog/2018/10/09/introducing-volume-snapshot-alpha-for-kubernetes/) to get you started.

# Attribution

My Kubernetes configuration was built from the work done by [Geoff Bourne](https://github.com/itzg) who maintains the canonical [Docker container](https://github.com/itzg/docker-minecraft-bedrock-server) which makes all of this possible. Thank you, Geoff! [Go follow him on Twitter](https://twitter.com/itzg), too.

[Google Cloud Platform]: https://cloud.google.com
[Cloud Shell]: https://console.cloud.google.com
[helm]: https://github.com/helm/helm/releases
[gcloud]: https://cloud.google.com/sdk
[kubectl]: https://kubernetes.io/docs/tasks/tools/install-kubectl/
[GKE]: https://cloud.google.com/kubernetes-engine/
[Kubernetes]: https://kubernetes.io
[GCE instance pricing]: https://cloud.google.com/compute/vm-instance-pricing#general-purpose_machine_type_family
[locations]: https://cloud.google.com/compute/docs/regions-zones#locations
[PVC Expansion]: https://kubernetes.io/blog/2018/07/12/resizing-persistent-volumes-using-kubernetes/
[docker-minecraft-bedrock-server]: https://github.com/itzg/docker-minecraft-bedrock-server
[Minecraft Bedrock Server]: https://www.minecraft.net/en-us/download/server/bedrock/

[^0]: Personally I love playing Java Edition but my kids have Minecraft on their iPhones. Considering this was written in from the depths of shelter-in-place COVID-19 lockdown my kids one.