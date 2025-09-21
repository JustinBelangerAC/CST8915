# Lab 2

- Video Link: https://www.youtube.com/watch?v=2HJ4vQ6aBRU
- Store-front git repo: https://github.com/JustinBelangerAC/store-front
- Product-service git repo: https://github.com/JustinBelangerAC/product-service
- Order-service git repo: https://github.com/JustinBelangerAC/order-service

---

- What changes did you make to the order-service and product-service to comply with the Configurations and Backing Services factors of the 12-Factor App methodology?
    1. Codebase
        - we split each service into their own git repo
        - this is important because it lets us make changes to 1 service without it affecting the others
    2. Dependencies 
        - when we split the services into each repo, we also split the dependencies
        this makes it so each service can scaled to run on different systems without needing to download redundant dependencies
        - this also makes it easier to develop the app, if we are tasked with working on only 1 of the services, we know exactly what deps we need to install, we also don't install the deps that we don't need for the service
    3. Config
        - instead of hard coding values like URL and port numbers in the code, we moved these to a .env file and load them into the system on startup
        - this makes the system more scalable, we don't need to change values and rebuild the app if we want to run a new instance of the service
    4. Backing services
        - we treat the RabbitMQ as it own service, we host it in its own VM
        - it doses't need its own repo because the RabbitMQ team is in charge of developing it
        - this makes more separation between the services
            - if we need to scale the system we can scale only the services that need to be scaled

- Why is it important to use environment variables instead of hard-coding configurations in your application?
    - if the application is already built and we only have a binary file, we won't be able to change the values
    - if we need to scale the system, we wont need to change the hard codded values on each instance and rebuild the app, we only need to change the .env files and relaunch

- Why is it important to have separate repositories for each microservice? How does this help maintain independence and scalability of each service?
    - its important because it lets each microservice be developed independently, 
    - during the CI/CD, we will only need to build the service that changed, we can fetch the other microservices binaries from the artifacts
    - it lets us roll back changes on a single service without needing to roll back the others
    - it makes the system easier to scale because if only 1 service needs to be scaled, we can create a new instance of just that service, no need to make 2 front end instances if the back-end is the only bottleneck
    - the independent repos for each service makes it so that we can have separate access control in the github, only the dev team in change of the service is able to make changes to it

Notes about setup challenges or lessons learned:
- The student subscription only allows up to 4 CPU cores per region
    - the fix for this is to host 1 of the VMs in another region
- when you specify a URL to connect to, its important to add HTTP://
- when you change something in an .env file, you need to relaunch the server