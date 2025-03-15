first set up the k8s cluster with the following github link, which contains terraform files for infrastructure creation
link:-

there is a script.sh attached to the masternode of the cluster 
it contains the installation of the following 
    - unzip , vim 
    - openjdk-17 (java)
    - maven
    - jenkins
    - docker
    - kubectl
    - awscli
    - aws-iam-authenticator
    - sonarqube docker container

if this script is attached it will install all necessary packages and tools

after all thats installed 

install argocd operator
here is the link of the operatorhub.io :- https://operatorhub.io/operator/argocd-operator
click on install and you will get the commands to install olm (operator lifecycle manager) and argocd operator

after argocd operator is installed then install argocd controllers 
here is the yaml file for creating basic argocd controllers

        apiVersion: argoproj.io/v1alpha1
        kind: ArgoCD
        metadata:
           name: example-argocd
           labels:
            example: basic
        spec:
         server:
          service:
            𝘁𝘆𝗽𝗲: LoadBalancer

use below command to apply
    kubectl apply -f <file_name>.yml

access the argocd web UI using the loadbalancer URL with below command 
    kubectl get svc
if is shows any risk click on advance and accept the risk

by default argocd username will be 'admin'
password will be stored in secrets 
    kubectl edit secrets <secret_aplication_name>
copy the secret as it will be in the base64 encoded format decode using below command 
    echo <encoded_password> | base64 -d


# sonarqube as a container
docker run -d -p 9000:9000 --name sonar sonarqube:lts


