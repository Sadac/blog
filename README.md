# blog
This is just a simple app to try out k8s and microservice architecture

## Create a pod to be deployed (example)
1. Build an image for the desired app
```bash
docker build -t dockeruser/image-name path
docker build -t roccosada/event-bus .
```
2. Push the image to the registry (dockerhub)
```bash
docker push roccosada/event-bus
```
3. Create a Deployment for the image creating a file `event-bus-depl.yaml` and apply it from the k8s folder
with `kubectl apply -f event-bus-depl.yaml` at this point we have our deploy and our pod created.
`kubectl get deployments` or `kubectl get pods` to verify.
At this point this pod doesn't have communication with any other pod of the node, we have to create a Service type in
order to establish communication
4. Create a Cluster IP service (a type of Service for communication between pods inside the cluster)
5. Wire it all up by

## Skaffold
Create a skaffold.yaml file and create the manifest, them apply it.
In the root of the `skaffold.yaml` file, execute
```sh
skaffold dev
```
You may need to run this command more than 2 times until you get the logs listening for the services.
At this point when the skaffold is up, you can made any changes to your code, save, and then skaffold will make all the required actions in order to get your codebase and images updated.
#### IMPORTANT
- Node services are auto updated on save because we use the nodemon dependency.
- client service is auto updated on save because we use create-react-app and this is an included feature.
So all of our services are using tools that are going to restart the primary process whenever sees a change to a file.
So we have 2 leves of restarting changes:
1. The file changed is taken by skaffold, and renew the image
2. The new image is using its own nodemon to restart the process

- If you terminate the skaffold process on terminal, all the kubernetes objects will get terminated. You won get deployments, services, pods, etc.
