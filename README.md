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
