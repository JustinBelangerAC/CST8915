# Lab 3

- Video link: https://www.youtube.com/watch?v=xF_l0pfEwcU&feature=youtu.be
- Order service link: https://github.com/JustinBelangerAC/order-service
- Product service link: https://github.com/JustinBelangerAC/store-front
- store-front link: https://github.com/JustinBelangerAC/store-front


1. What challenges did you encounter when configuring environment variables in the GitHub Actions workflow?
    - My store-front was not working properly so I made a new instance of static-web-app
        - this changed the API key and made a new yaml file
        - when i tried to add the env vars to that yaml file, i copied the entire last one into the new one (keeping the old API key)
        - the fix for this was easy, just restore the old file and add the env vars
2. How does deploying microservices on Azure Web App Service differ from running them locally?
    - don't need to create VMs or wait for them to boot up
    - the github actions take a long time (not as long as VMs though)
        - the github pipeline to deploy the app was about 1 minute
        - with azure web app, i can't SSH into the machine to see if its running properly or to diagnose problems
            - the service has logs to do that, but you cant run commands from there to my knowledge
    - you don't need to create an env file, you just do it in the Azure UI or a yml file
3. Why is it important to use environment variables for configurations in a cloud environment?
    - hardcoding the variables is bad because when we build the app, the variables will be stuck in the binary file and won't be able to change
    - if we want to scale by adding a new instance of the service, we wont be able to access it because the ports and IPs are hard coded
    - this is called tight coupling, when each service relies heavily on each other
        - the 12 factors want us to have louse coupling so that we can interchange each microservice without needing to change the code in the other services
