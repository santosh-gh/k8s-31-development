# Part 31: Deploy microservices on Azure Kubernetes Service using Helm charts stored in HelmRepository (ACR), Build and Push Docker Images and Helm Charts through Azure   Pipelines. Manage delivery using Flux CD with image automation. Tag images with Semantic Version.

    Part1:   Manual Deployment (AzCLI + Docker Desktop + kubectl)  
    GitHub:  https://github.com/santosh-gh/k8s-01
    YouTube: https://youtu.be/zoJ7MMPVqFY

             - Good for learning and small projects.
             - Error-prone due to manual steps.
             - Not scalable for teams or large projects.

    Part2:   Automated Deployment (AzCLI + Docker + kubect + Azure Pipeline)
    GitHub:  https://github.com/santosh-gh/k8s-02
    YouTube: https://youtu.be/nnomaZVHg9I

            - Faster, repeatable deployments.
            - Reduces human error.
            - Integrates CI/CD best practices.

    Part3:   Automated Infra Deployment (Bicep + Azure Pipeline)
    GitHub:  https://github.com/santosh-gh/k8s-03
    YouTube: https://www.youtube.com/watch?v=5PAdDPHn8F8

    Part4:   Manual Deployment (AzCLI + Docker Desktop + Helm charts + kubectl) 
    GitHub:  https://github.com/santosh-gh/k8s-04
    YouTube: https://www.youtube.com/watch?v=VAiR3sNavh0

             - need to maintain separate files for each environment.
             - No concept of packaging/distribution.
             - no built-in rollback or release tracking.

    Part5:   Automated Deployment (AzCLI + Docker + Helm charts + kubectl + Azure Pipeline) 
    GitHub:  https://github.com/santosh-gh/k8s-04
    YouTube: https://www.youtube.com/watch?v=MnWe2KGRrxg&t=883s

             - Helm uses templates and values (values.yaml) ? same chart can deploy multiple 
               environments (dev, staging, prod) with different configs.
             - Helm packages apps as charts, which can be versioned, shared, and 
               stored in repositories (like Docker images).
             - Helm tracks releases ? easy to upgrade, rollback, and list installed versions 
               (helm upgrade, helm rollback).               
             - Helm can bundle multiple Kubernetes resources (Deployments, Services, Ingress, ConfigMaps, etc.) 
               into a single chart ? deploy everything with one command.

    Part6:   Automated Deployment (AzCLI + Docker + Helm charts + kubectl + Azure Pipeline) 
             Dynamically update the image tag in values.yaml
    GitHub:  https://github.com/santosh-gh/k8s-06
    YouTube: https://www.youtube.com/watch?v=Nx0defm8T6g&t=11s

    Part7:   Automated Deployment (AzCLI + Docker + Helm charts + kubectl + Azure Pipeline)
             Store the helm chart in ACR
             Dynamically update the image tag in values.yaml
             Dynamically update the Chart version in Chart.yaml

    GitHub:  https://github.com/santosh-gh/k8s-07
    YouTube: https://www.youtube.com/watch?v=Y3RaxSZNTaU&t=1s

    Part8:   Automated Deployment (AzCLI + Docker + Helm charts + kubectl + Azure Pipeline)
             Store the helm chart in ACR
             Dynamically update the image tag in values.yaml
             Dynamically update the Chart version in Chart.yaml
             Deploy into multiple environments (dev, test, prod) with approval gates

    GitHub:  https://github.com/santosh-gh/k8s-08
    YouTube: https://www.youtube.com/watch?v=oNysAAGijGk&t=43s

    Part9:   Manual Deployment (AzCLI + Docker + kustomize + kubectl)          
             Deploy into multiple environments (dev, test, prod) through command line

    GitHub:  https://github.com/santosh-gh/k8s-09
    YouTube: https://www.youtube.com/watch?v=Jtz1KldOPAA&t=1s

             - Overlay-based approach makes managing multiple environments (dev, staging, prod) 
               straightforward via Git branches/overlays.

    Part10:  Automated Deployment (AzCLI + Docker + kustomize + kubectl + Azure Pipeline)          
             Deploy into multiple environments (dev, test, prod) through automated pipeline

    GitHub:  https://github.com/santosh-gh/k8s-10
    YouTube: https://www.youtube.com/watch?v=m5ZXmOk0IBs&t=43s

    Part11:  Manual Deployment (AzCLI + Docker + Helm + kustomize + kubectl)          
             Deploy into multiple environments (dev, test, prod) using command line tools.

             - Helm = packaging + release mgmt (install/upgrade/rollback)
             - Kustomize = environment overlays (patches/config differences)
             - Together = scalable, reusable, environment-flexible microservice deployment strategy


    GitHub:  https://github.com/santosh-gh/k8s-11
    YouTube: https://www.youtube.com/watch?v=ZNHoZ_b85DQ&t=1s

    Part12:  Automated Deployment (AzCLI + Docker + Helm + kustomize + kubectl)
             Template First approach 
             Dynamically update the image tag in deploy.yaml         
             Deploy into multiple environments (dev, test, prod) using Azure Pipeline.

    GitHub:  https://github.com/santosh-gh/k8s-12
    YouTube: https://www.youtube.com/watch?v=qxJyTHzWG4U

    Part13:  Manual Deployment (AzCLI + Docker + Helm + kustomize + kubectl)
             Overlay First approach             
             Deploy into multiple environments (dev, test, prod) thorough commands.

    GitHub:  https://github.com/santosh-gh/k8s-13
    YouTube: https://www.youtube.com/watch?v=9uAM8FgNGmI&t=113s

    Part14:  Automated Deployment (AzCLI + Docker + Helm + kustomize + kubectl)
             Overlay First approach             
             Deploy into multiple environments (dev, test, prod) thorough Azure Pipeline.

    GitHub:  https://github.com/santosh-gh/k8s-14
    YouTube: https://www.youtube.com/watch?v=VAiR3sNavh0

    Part15: ArgoCD (Create Argo CD app using UI and Dashboard)
            Create Argo CD applications using Argo CD UI and Dashboard 

            Manual methods: Best for learning, experimentation, and very small projects.
            Automated methods: Best for production, team collaboration, and scaling.   

            kubectl: Simple no extra tools or templating engines needed.

            Helm:  Best for packaging, reusability, upgrades and rollbacks.                    
                can use reusable and ready-made chart.

            Kustomize: Best for environment-specific overlays without duplicating YAML.
                    Patch existing YAMLs for different environments.
                    Powerful when you need to tweak a vendor Helm chart

            Helm + Kustomize: Very flexible, but complex; fits for large enterprises.


            # Traditional Deployment: PUSH Approach

              - Requires the pipeline runner or command line to have cluster credentials
              - The live state may drift from the intended state
              - Rollback means re-running a previous pipeline, manually applying manifests, or 
                keeping Helm release history.
              - Usually requires custom scripting to target multiple clusters (e.g., staging, prod).

            # GitOps(ArgoCD) Deployment: PULL Approach
              
              - Runs inside the cluster and pulls changes from Git.
              - Git is the single source of truth for manifests.
                Detects drift and can automatically fix it.
              - Simply revert the Git commit, Argo syncs back to the previous state.
              - Can promote changes from dev -> test -> prod simply by managing Git branches or directories.
              - Provides a dashboard/UI showing real-time status (Healthy, OutOfSync, Degraded).

    GitHub:  https://github.com/santosh-gh/k8s-15  
    YouTube: https://www.youtube.com/watch?v=Cnt5RZ5m3l8&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=15

    Part16: ArgoCD (Create Argo CD app using UI and Dashboard, continue on Part15)
            Create Argo CD applications using Argo CD UI and Dashboard
    GitHub:  https://github.com/santosh-gh/k8s-16
    YouTube: https://www.youtube.com/watch?v=GYMY4ZQ7V9o&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=16

    Part17: ArgoCD (Create Argo CD app using manifest)
            Create Argo CD applications using manifests (CRD - Application)
    GitHub:  https://github.com/santosh-gh/k8s-17
    YouTube: https://www.youtube.com/watch?v=W-s6A61w7BI&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=17

    
    Part18: ArgoCD (Create Argo CD app using manifest)
            Create Argo CD applications using manifests
            Create Argo CD applications using manifests (CRD - ApplicationSet)
    GitHub:  https://github.com/santosh-gh/k8s-18
    YouTube: https://www.youtube.com/watch?v=3ppWmlnFP8U&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=18

    Part19: ArgoCD (Automate deployment using Azure Pipeline)
            Create Argo CD applications using manifests
            Helmchart
            Automate deployment using Azure Pipeline

    GitHub:  https://github.com/santosh-gh/k8s-19-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-19-deployment.git
    YouTube: https://www.youtube.com/watch?v=c6ZZNgKLh6g&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=19

    Part20: ArgoCD (Automate deployment using Azure Pipeline)
            Create Argo CD applications using manifests 
            CRD - ApplicationSet
            Helmchart
            Automate deployment using Azure Pipeline

    GitHub:  https://github.com/santosh-gh/k8s-20-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-20-deployment.git
    YouTube: https://www.youtube.com/watch?v=bzCk-tDUlZc&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=20

    Part21: ArgoCD (Automate deployment using Azure Pipeline)
            Create Argo CD applications using manifests 
            CRD - ApplicationSet
            Kustomize
            Automate deployment using Azure Pipeline

    GitHub:  https://github.com/santosh-gh/k8s-21-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-21-deployment.git
    YouTube: https://www.youtube.com/watch?v=ILNxCQ5VZ4g&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=21

    Part22: GitOps using Flux (Microservice deployment using Flux, KinD)

    GitHub:  https://github.com/santosh-gh/k8s-21-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-22-deployment.git
    YouTube: https://www.youtube.com/watch?v=hdxo5uw35vs&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=22

    Part23: GitOps using Flux (Microservice deployment using Flux, KinD)

    GitHub:  https://github.com/santosh-gh/k8s-21-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-23-deployment.git
    YouTube: https://www.youtube.com/watch?v=98gdG70yjmU&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=23

    Part24: GitOps using Flux (Microservice deployment using Flux, Kustomization)
            Deploy into multiple environments (dev,test and prod)

    GitHub:  https://github.com/santosh-gh/k8s-21-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-24-deployment.git
    YouTube: https://studio.youtube.com/video/hdxo5uw35vs/edit

    Part25: GitOps using Flux (Microservice deployment using Flux, Helm Chart)             
             Single Helm Chart with multiple Microservices

    GitHub:  https://github.com/santosh-gh/k8s-21-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-25-deployment.git
    YouTube: https://www.youtube.com/watch?v=rouNQMR-4P8&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=25  

    Part26: GitOps using Flux (Microservice deployment using Flux, Helm Chart)             
            Helm Chart with multiple Microservices
            Deploy into multiple environments dev, test and prod

    GitHub:  https://github.com/santosh-gh/k8s-21-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-26-deployment.git
    YouTube: https://www.youtube.com/watch?v=NpS63UEO3Bg&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=26 

    Part27: GitOps using Flux (Microservice + Flux + Helm Chart + Kustomize)             
            Helm Chart with multiple Microservices
            Deploy into multiple environments dev, test and prod

    GitHub:  https://github.com/santosh-gh/k8s-21-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-27-deployment.git
    YouTube: https://www.youtube.com/watch?v=QboicrPivH4&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=27

    Part28: GitOps using Flux (Microservice + Flux + Helm Chart + HelmRepository(GHCR) + KinD)             
            Helm Chart with multiple Microservices
            Helm Charts in HelmRepository (GitHub Container Registry)
            OCI
            Private Repository

    GitHub:  https://github.com/santosh-gh/k8s-28-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-28-deployment.git
    YouTube: https://www.youtube.com/watch?v=WTJvum3IZTU&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=28 

    Part29: GitOps using Flux (Microservice + Flux + Helm Chart + HelmRepository(ACR)+ AKS)             
            Helm Chart with multiple Microservices
            Helm Charts in HelmRepository (Azure Container Registry)
            OCI
            Private Repository

    GitHub:  https://github.com/santosh-gh/k8s-29-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-29-deployment.git
    YouTube: https://www.youtube.com/watch?v=WcY1XZb4_J8&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=29 

    Part30: GitOps using Flux (Microservice + Flux CD + Helm Chart + HelmRepository(ACR) + Image Automation + AKS)             
            Helm Chart with multiple Microservices
            Helm Charts in HelmRepository (Azure Container Registry)
            Flux Image Automation
            OCI
            Private Repository
    GitHub:  https://github.com/santosh-gh/k8s-30-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-30-deployment.git
    YouTube: https://www.youtube.com/watch?v=NpS63UEO3Bg&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=26

    Part31: GitOps using Flux (Microservice + Flux CD + Helm Chart + HelmRepository(ACR) + Image Automation + AKS + Azure Pipeline)             
            Helm Chart with multiple Microservices
            Helm Charts in HelmRepository (Azure Container Registry)
            Azure Pipeline for build and push docker images and helm charts to Azure container Registry
            Use Semantic version for image tag
            Manage delivery using Flux CD with image automation
            Private Repository (OCI)
    GitHub:  https://github.com/santosh-gh/k8s-30-development.git     
    GitHub:  https://github.com/santosh-gh/k8s-30-deployment.git
    YouTube: https://www.youtube.com/watch?v=NpS63UEO3Bg&list=PLr6ErUeFySVug9VG73_W2MypRez_ZycWh&index=26

# Architesture

![Store Architesture](aks-store-architecture.png)

    # Store front: Web application for customers to view products and place orders.
    # Product service: Shows product information.
    # Order service: Places orders.
    # RabbitMQ: Message queue for an order queue.

# Tetechnology Stack
   
    AKS
    ACR
    docker desktop
    git hub
    kubectl
    Flux CD   

# Prerequisites

  Install Docker

  GitHub CLI

  Install kubectl

# Infra Deployment

  # Login to Azure
  az login
  az account set --subscription=<subscriptionId>
  az account show

  # Show existing resources
  az resource list

  # Create RG, ACR and AKS using AzCLI
  ./infra/azcli/script.sh

  OR

  #  Create RG, ACR and AKS using Bicep
  az deployment sub create --location uksouth --template-file ./infra/bicep/main.bicep --parameters ./infra/bicep/main.bicepparam

  # Connect to cluster
  RESOURCE_GROUP="rg-onlinestore-dev-uksouth-001"
  AKS_NAME="aks-onlinestore-dev-uksouth-001"
  az aks get-credentials --resource-group $RESOURCE_GROUP --name $AKS_NAME --overwrite-existing

  # Short name for kubectl
  alias k=kubectl

  # Show all existing objects
  k get all

# Log in to ACR
  ACR_NAME="acronlinestoredevuksouth001"
  az acr login --name $ACR_NAME

# Build and push the Docker images to ACR

  # Order Service
  docker build -t order ./app/order-service 
  docker tag order:latest $ACR_NAME.azurecr.io/order:1.0.0
  docker push $ACR_NAME.azurecr.io/order:1.0.0

  # Product Service
  docker build -t product ./app/product-service 
  docker tag product:latest $ACR_NAME.azurecr.io/product:1.0.0
  docker push $ACR_NAME.azurecr.io/product:1.0.0

  # Store Front Service
  docker build -t store-front ./app/store-front 
  docker tag store-front:latest $ACR_NAME.azurecr.io/store-front:1.0.2
  docker push $ACR_NAME.azurecr.io/store-front:1.0.2

  docker images

# Helm Push and Install
  OCI refers to the Open Container Initiative, a lightweight, open governance 
  structure that defines open industry standards for container formats and runtimes. 

  export HELM_EXPERIMENTAL_OCI=1
  On Helm v3.8.0 and later, OCI is supported by default — no environment variable needed.

  helm registry login $ACR_NAME.azurecr.io

  helm package ./multi-helmchart/config
  helm package ./multi-helmchart/rabbitmq
  helm package ./multi-helmchart/order
  helm package ./multi-helmchart/product
  helm package ./multi-helmchart/store-front

  helm push config-0.1.0.tgz oci://$ACR_NAME.azurecr.io/online-store-charts
  helm push rabbitmq-0.1.0.tgz oci://$ACR_NAME.azurecr.io/online-store-charts
  helm push order-0.1.0.tgz oci://$ACR_NAME.azurecr.io/online-store-charts
  helm push product-0.1.0.tgz oci://$ACR_NAME.azurecr.io/online-store-charts
  helm push store-front-0.1.0.tgz oci://$ACR_NAME.azurecr.io/online-store-charts

  helm push store-front-0.1.4.tgz oci://$ACR_NAME.azurecr.io/online-store-charts

  helm pull oci://$ACR_NAME.azurecr.io/helm/config --version 0.1.0
  helm pull oci://$ACR_NAME.azurecr.io/helm/rabbitmq --version 0.1.0
  helm pull oci://$ACR_NAME.azurecr.io/helm/order --version 0.1.0
  helm pull oci://$ACR_NAME.azurecr.io/helm/product --version 0.1.0
  helm pull oci://$ACR_NAME.azurecr.io/helm/store-front --version 0.1.0

  helm install config-release oci://$ACR_NAME.azurecr.io/helm/config --version 0.1.0
  helm install rabbitmq-release oci://$ACR_NAME.azurecr.io/helm/rabbitmq --version 0.1.0
  helm install order-release oci://$ACR_NAME.azurecr.io/helm/order --version 0.1.0
  helm install product-release oci://$ACR_NAME.azurecr.io/helm/product --version 0.1.0
  helm install store-front-release oci://$ACR_NAME.azurecr.io/helm/store-front --version 0.1.0

# Install Flux CLI

    Windows:
    choco install flux

    Mac:
    brew install fluxcd/tap/flux

    Linux:
    curl -s https://fluxcd.io/install.sh | sudo bash

    flux --version

# FluxCD Prerequisites Check
  flux check --pre

# Install Flux in Cluster

# GitHub
  gh auth login
  gh repo create <repo-name> --public 

# Bootstrap Flux in the Cluster

  Creating a GitHub Personal Access Token (PAT)

  export GITHUB_USER='santosh-gh'
  export GITHUB_REPO='k8s-27-deployment'
  export GITHUB_TOKEN=<pat-token>

  flux bootstrap github \
    --owner=$GITHUB_USER \
    --repository=$GITHUB_REPO \
    --branch=main \
    --path=clusters/demo-cluster \
    --personal=true \
    --private=false

    Create a Git repo 

    Install the Flux components in Kubernetes cluster.

    Configure Flux to reconcile manifests underclusters/demo-cluster/
    
    
  k get pods -n flux-system
  k get all -n flux-system

# FluxCD Components

  Flux - the primary operator (control plane), continuously monitoring the Git repository 
          and applying changes to the Kubernetes cluster.

  Kustomize Controller - supports managing Kubernetes manifests using Kustomize,
                         also enabling customize the deployments.

  Source Controller - monitors the source of the Kubernetes manifests (Git, Helm repositories, etc.) 
                      and makes them available for the other controllers.

  Helm Controller - responsible for managing Helm artifacts.

  Notification Controller - handles notifications and alerts for deployments

 # Setting Up FluxCD to Deploy the Application
    
    # Microservice Manifests
    # Create a Kustomization File
    # Link the Application Directory to FluxCD

# Commit and Push to Repository

# Verify FluxCD Reconciliation
  Trigger Reconciliation:
  flux reconcile kustomization flux-system -n flux-system

  Check Logs:
  kubectl logs -n flux-system deploy/kustomize-controller

  Check Kustomization Status:
  flux get kustomizations -n flux-system

  flux get kustomizations --watch
  flux get kustomizations -w

  flux get sources git
  flux get kustomizations

  Check that the app was created:
  kubectl get all

  flux events

# Flux Sync

  kubectl get kustomizations -n flux-system
  flux get kustomizations

# Uninstall Flux

# Delete Cluster

kind delete cluster --name demo-cluster



export GITHUB_USER='santosh-gh'




helm registry login ghcr.io -u $GITHUB_USER --password-stdin

OR 

helm registry login ghcr.io \
  --username $GITHUB_USER \
  --password $GITHUB_TOKEN

helm package ./multi-helmchart/config
helm package ./multi-helmchart/order
helm package ./multi-helmchart/product
helm package ./multi-helmchart/rabbitmq
helm package ./multi-helmchart/store-front

helm push config-0.1.0.tgz oci://ghcr.io/santosh-gh/online-store-charts
helm push order-0.1.0.tgz oci://ghcr.io/santosh-gh/online-store-charts
helm push product-0.1.0.tgz oci://ghcr.io/santosh-gh/online-store-charts
helm push rabbitmq-0.1.0.tgz oci://ghcr.io/santosh-gh/online-store-charts
helm push store-front-0.1.0.tgz oci://ghcr.io/santosh-gh/online-store-charts

helm push order-1.0.0.tgz oci://ghcr.io/santosh-gh/online-store-charts


helm pull oci://ghcr.io/santosh-gh/online-store-charts/order --version 0.1.0


kubectl create secret docker-registry ghcr-helmchart-secret \
  --namespace=flux-system \
  --docker-server=ghcr.io \
  --docker-username=$GITHUB_USER \
  --docker-password=$GITHUB_TOKEN \
  --docker-email=santosh.mohapatra25@gmail.com

helm show all oci://ghcr.io/santosh-gh/helm-charts/online-store --version 1.0.0

flux logs -n flux-system | grep online-store-repo
