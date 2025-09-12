# Lab 1

1. make a short video
    - [here is the link to my video](https://www.youtube.com/watch?v=cqkTl8-jWvg) 

2. Brief technical explanation

    for each service, write a technical explanation

    1. Order service
        - what is the service responsible for?

            This service works like a bridge between the UI and the message queue. We don't want to expose the database IP to the user for security reasons, we need a middle ground to perform validation before sending it to the DB. 

        - what language does this use?

            This uses JavaScript to use Node.js, node lets us code servers using javascript.

        - how does it interact with the other services

            At the moment, this  service takes requests from the user interface (store-front), it reads requests that come into 3000/orders, it will read the JSON from the body of the request and send it over to the RabbitMQ service

    2. Product service
        - what is the service responsible for?
            
            the order service is responsible for storing the products that we are selling. It's sort of like a database, but it only stores an array 3 of JSON objects representing the products. you can only fetch things from this "DB" you can't add or modify anything, its all hardcoded.
            
        - what language does this use?

            This service uses RUST, its a low level programming language, this means it operates closer to the bare metal of the machine when compared to languages like C# and Java.

        - how does it interact with the other services

            This service only talks with the front end user interface, it only listens on 3030/products, if it gets all call it will return the hardcoded JSON array of product information. When the user interface is loaded, this call is made to populate the list of available products.

    3. RabbitMQ
        - what is the service responsible for?

            This service is meant to work as a middle ground between the order service and a DB, there is no real DB at the moment. This is important because if we send tons of async requests to the DB, it will get confused and jumble up the IDs. We need a message queue so that the DB requests happen 1 at a time

        - what language does this use?

            This is a free application that we downloaded. Google tells me that it is written in Erlang and is built on the Open Telecom Platform framework.

        - how does it interact with the other services

            This service takes requests from order services containing the products that the user ordered and would send them over to a DB but there is none. At the moment the queue is never emptied, the data lives there forever and ever (until I decide to pull the plug on the VM)

    4. Store front
        - what is the service responsible for?

            This service is where the UI is hosted, when a user connects to this service, they get a web page where they can order pet food. This is where the users can interact with the system.

        - what language does this use?

            This uses Javascript, HTML, and CSS. The vue.js framework lets us create components and bundle them up to make the UI.

        - how does it interact with the other services

            When the web page is loaded, it will try and fetch the list of products from products service, if it can't it will tell the user that something went wrong.

            When a user tries to buy a product, it will bundle up all the product information in the UI and make a JSON object containing the ID, Product name, Price and quantity, this JSON object will be sent over to the order service where it will be sent to the msg queue
