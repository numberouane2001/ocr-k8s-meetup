# ocr-k8s-meetup
k8s deployment files
Those files contains the k8s definition files to deploy a small app analysing the Meetup activities in France.


PREREQUISITES:
In order to create the application resources in k8s, first ensure that you have a k8s cluster working.
Note, it has been tested on AWS AKS cluster and an on premise k8s 1.14 cluster.
It uses statefulset applications. This kind of deployment requires that a dynamic storage solution has been setup on the k8s cluster. You can use for this glusterfs, storageos,... Please refer to the k8s documentation for more details.
It requires that you have kubectl installed and configured to connect to your k8s cluster.

CONTENT:
Those files deploys:
- dynamic storage class
- a zookeeper cluster
- a kafka cluster
- a cassandra cluster
- a python pod downloading city definition from Meetup
- a python pod downloading upcomingevents from Meetup
- a kafka streams pod inserting in cassandra the parsed cities definition
- a kafka streams pod inserting in cassandra the parsed events definition
- deployment and a loadbalancer with an embedded web server retrieving the Top 3 of the most active cities on Meetup on the last month.

DEPLOYMENT:
In order to deploy the application, run the following command:
kubectl create -f https://github.com/numberouane2001/ocr-k8s-meetup.git

TESTING THE APPLICATION:
Check the status of the pods using 
kubectl get po -o wide

You can retrieve the external access to the web service of the application using 
kubectl get services -o wide
It should display a LoadBalancer service/results. Copy the external IP, the tcp port and use it in Firefox to access to the HTTP page result.

APPLICATION CLEANING:
In order to cleanup the application, run the following command:
kubectl delete -f https://github.com/numberouane2001/ocr-k8s-meetup.git

