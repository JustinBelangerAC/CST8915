# Lab8

Here is my video link: https://youtu.be/8kbLdK5Phoc
- I could not figure out how to make rabbitMQ persistent, I do not know what is wrong with my configuration

## Azure managed MongoDB

### Azure blob storage
- Stores unstructured data
- Super easy to configure (no need to mess with volumes)
- Cheaper to run
- Easy to setup high availability (no need to setup replicas)
- Easy to setup backups (if aks goes down, the volumes do too)

### Azure CosmosDB
- Stores unstructured data with very low latency, scalable worldwide
- Super easy to configure (no need to mess with volumes)
- Super easy to scale and create replicas in new areas
- Easy to setup high availability (no need to setup replicas)
- Automatic backups (if aks goes down, the volumes do too)


## Azure managed RabbitMQ

### Azure Service bus
- Is a messaging queue, can also support pubsub
- Easy to setup (can use the portal or IaC, no need to mess with k8s volumes)
- Easy to scale to meet demands (no need to worry about replicas)
- Easy high availability (no need to make sure that the replicas have persistent / shared storage)