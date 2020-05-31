# k8-docker-desktop-kafka

### Summary
This repo contains a docker-compose file for running Zookeeper and a Kafka broker. There are feature branches to extend the cluster to include Kafka Connect, Kafka Proxy, and Kafka KSQL (These are all Confluent tools).
The main reason for this repo is simple way to startup Kafka in a local dev env running in Kubernetes. Those intstructions will  be listed in this README.
NOTE: 
I am running the edge version of Docker. I read that you don't need the edge version anymore to run Docker in Kubernetes but if some of the following instructions don't match that is why.

### Prerequisits
1. Docker
2. Kubctl (brew install kubctl)
3. Kafka tools (brew install Kafka -- don't start Kafka once the tools are installed).

## Installation/Run Instructions
1. Install Docker Desktop (these instructions are for Mac OSX. Windows and Linux users might still get some value out of this... but the instructions aren't tested)
2. On Docker icon on the top menu bar click and select preferences. 
3. Once preferences opens, choose Kubernetes,  click the checkbox next to Enable Kubernetes and Deploy Docker Stacks to Kubernetes by default.
4. Apply and Restart
5. In the root directory of this project run docker-compose pull.
6. Deploy the docker-compose stack to Kubernetes like so: 
```docker stack deploy --compose-file docker-compose.yml kafka-stack```
7. If kubctl was installed properly, you should be able to run these commands and see the running pods and services:
```kubectl get svc ```
```kubectl get pods ```
8. There are a few ways to clean up and start fresh. You can either remove the stack or, a bit more heavy, reset the Kubernetes cluster through the Docker preferences:
``` docker stack rm kafka-stack```
or go to preferences and reset Kubernetes. 
9. Start the Kubernetes dashboard:
``` kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml```
From the terminal command line run the proxy command: 
``` kubectl proxy ```
go to this URL: 
``` http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/ ```
10. Use the token to authenticate. Your secret can be retrieved with this command: 
``` kubectl -n kube-system describe secret default | grep "token:"```
Use that token for authentication for the dasboard. 



## Issues/To Dos



## Notes
There are many other methods to run Kubernetes locally including minikube (kinda big resource footprint), Kind (pretty awesome but very light), or many others. This is probably the quickest way to get Kubernetes going with Kafka.
To use other Confluent tools like Schema-Registry, Connect, and Kafka proxy, go to this release branch and refresh your Kubernetes environment with the docker-compose file on that branch. 
``` feature/confluent-tools```



## Related Projects/Dependencies
Related or project dependenices
