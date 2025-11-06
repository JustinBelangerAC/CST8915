# Lab 7

Here is my youtube video link: https://youtu.be/fgUQc0aod0s


1. Whether RabbitMQ is a stateless or stateful application
    - RabbitMQ is a stateful application, it stores the data for each message in the queue inside the RAM (this represents the state of the application)
    - it is recommended to have a storage microservice like a cache or DB instead of stateful applications so that the data can remain between deprovisioning of the service
2. The implications of running RabbitMQ without persistent storage
    - without persistent storage, RabbitMQ would not be able to keep its data when it is deleted
    - let's say that we are scaling the RabbitMQ service to handle peak load, when we decide to deprovision some of the copies to match normal load, some of the data would be lost 
    - persistent storage in the cluster would allow each copy of RabbitMQ to share the messages that they get in a centralized source, ensuring that data can remain when resources are deleted and that the data is consistent
3. What happens when the RabbitMQ pod is deleted or restarted
    - When RabbitMQ is deleted or restarted the write layer of the container that it runs in is lost
    - this means that the messages in the queue are gone, this makes it hard to scale down the application
4. Potential solutions to this problem (research-based)
    - adding a persistent storage to the cluster where all messages from RabbitMQ are sent so that the data is not deleted with the containers, this storage would also make sure that the messages are consistent. I was running into an issue where the rabbitMQ page showing the number of messages was always different because it was getting that number from 6 different pods. The UI was showing a different number every time it was polling the pods. a persistent storage and a different UI for seeing the messages would allow us to have an accurate number of TOTAL messages
    - using a managed service for the messaging queue microservice would resolve the scaling issues by having all the data be managed by a provider. when we fetch the data, it would show every message for every instance of the queue
5. Does using Azure Service Bus solve the issues identified with RabbitMQ Configuration in this Lab?
    - Azure Service Bus is a managed service, the data for each message is managed by Azure, (the storage is Microsoft's problem).
    - this means that when we scale down, there won't be data loss
