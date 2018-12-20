# Kubernetes cookbook
## CI/CD
1. [Kubernetes - CI/CD - GCP - Jenkins architecture](https://cloud.google.com/solutions/continuous-delivery-jenkins-kubernetes-engine)
2. [Continuous-Delivery-Kubernetes-Google-Cloud-Build](https://stephenmann.io/post/continuous-delivery-using-google-kubernetes-engine-and-google-cloud-build/)
3. [gcp-kubernetes-source-to-prod](https://www.spinnaker.io/guides/tutorials/codelabs/gcp-kubernetes-source-to-prod/)

# kubernetes-standard
[Translate a Docker Compose File to Kubernetes Resources](https://kubernetes.io/docs/tasks/configure-pod-container/translate-compose-kubernetes/#build-and-push-docker-images)

[[LAB] Build and Deploy a Docker Image to a Kubernetes Cluster](https://www.qwiklabs.com/focuses/1738?locale=en&parent=catalog)

[Running Kubernetes on Google Compute Engine](https://kubernetes.io/docs/setup/turnkey/gce/)

[Cloud builder step](https://github.com/GoogleCloudPlatform/cloud-builders/tree/master/kubectl)

[Kubernetes best practice](https://www.weave.works/blog/kubernetes-best-practices)

# relevant stackoverflow
[Auto deploy when Image was created](https://stackoverflow.com/questions/46349803/is-there-a-way-to-automatically-deploy-to-gce-based-on-a-new-image-being-created)

# search keywords
[step by step deploy image to GCE by kubernetes](https://www.google.com/search?q=step+by+step+deploy+image+to+GCE+by+kubernetes&client=firefox-b-ab&ei=PDTZW-CrHMby8AWSqpeQCA&start=10&sa=N&ved=0ahUKEwjgub6q8K_eAhVGObwKHRLVBYIQ8tMDCLUB&biw=1920&bih=916)

# How to create secret from json in kubernetes?
1.  [Secret, ConfigMap from Json](https://medium.com/google-cloud/kubernetes-configmaps-and-secrets-part-2-3dc37111f0dc)
2.  [Using kubernetes secret](https://medium.com/platformer-blog/using-kubernetes-secrets-5e7530e0378a)

# Cloud builders - CI/CD

1.  [Continuous Delivery Using Google Kubernetes Engine and Google Cloud Build](https://stephenmann.io/post/continuous-delivery-using-google-kubernetes-engine-and-google-cloud-build/)
2.  [Configuring the order of build steps](https://cloud.google.com/cloud-build/docs/configuring-builds/configure-build-step-order)
3.  [Building, Testing, and Deploying Artifacts](https://cloud.google.com/cloud-build/docs/configuring-builds/build-test-deploy-artifacts)
4.  [Build, test, and deploy with Pipelines](https://confluence.atlassian.com/bitbucket/build-test-and-deploy-with-pipelines-792496469.html)
5.  [Check build status in a pull request](https://confluence.atlassian.com/bitbucket/check-build-status-in-a-pull-request-945541505.html)
6.  [Google Kubernetes Engine + Google Cloud Builder + GitHub for easy and quick CD pipeline](https://itnext.io/google-kubernetes-engine-google-cloud-builder-github-for-easy-and-quick-cd-pipeline-8aca663f1118)
7.  [Using Kubernetes namespaces to manage](https://kubernetes.io/blog/2015/08/using-kubernetes-namespaces-to-manage/)
8.  [Pre kubernetes engine for prod](https://cloud.google.com/solutions/prep-kubernetes-engine-for-prod)
9.  ...
# Gcloud command:

`gcloud container clusters get-credentials cloud-build-screening --zone=us-central1-b`

`gcloud auth configure-docker`

`kubectl create `

# Switch kubectl between Gcloud and local

`kubectl config use-context CONTEXT_NAME`

# to find context name 

`kubectl config get-contexts`

# namespace
[Kubernetes best practice organizing](https://cloud.google.com/blog/products/gcp/kubernetes-best-practices-organizing-with-namespaces?hl=no)
[Kubernetes – How to Create / Delete Namespaces; Why Namespaces?](https://vitalflux.com/kubernetes-create-delete-namespaces-namespaces/)


# docker-for-desktop

[web hook relay token](https://my.webhookrelay.com/tokens)



# Deploy spring cloud 
[deploying_using_kubectl](https://docs.spring.io/spring-cloud-dataflow-server-kubernetes/docs/1.4.0.RELEASE/reference/htmlsingle/#_deploying_using_kubectl)

[quick-guide-to-microservices-with-kubernetes-spring-boot-2-0-and-docker](https://piotrminkowski.wordpress.com/2018/08/02/quick-guide-to-microservices-with-kubernetes-spring-boot-2-0-and-docker/comment-page-1/#comment-1327)
# Spring cloud
[spring-cloud-consul](https://www.baeldung.com/spring-cloud-consul)


##  Any there any document for kubelet RESTAPI?
[openapi and swwager definition](https://kubernetes.io/docs/concepts/overview/kubernetes-api/#openapi-and-swagger-definitions)

##  Spring and kubernetes tutorial from Red hat
https://access.redhat.com/documentation/en-us/red_hat_jboss_fuse/6.3/html/fuse_integration_services_2.0_for_openshift/kube-spring-boot

##  [get-automatic-https-with-lets-encrypt-and-kubernetes-ingress](https://akomljen.com/get-automatic-https-with-lets-encrypt-and-kubernetes-ingress/)
##  [SSL/TLS cert on kubernetes](https://github.com/hungbang/cert-manager)
##  [AUTO PROVISIONING OF LETSENCRYPT TLS](https://medium.com/@maninder.bindra/auto-provisioning-of-letsencrypt-tls-certificates-for-kubernetes-services-deployed-to-an-aks-52fd437b06b0)
##  [INGRESS NGINX TLS USER GUIDE](https://kubernetes.github.io/ingress-nginx/user-guide/tls/)
# Recommendation 
##  [gke-letsencrypt](https://github.com/ahmetb/gke-letsencrypt)
# [secure-kubernetes-services-with-ingress-tls-letsencrypt](https://docs.bitnami.com/kubernetes/how-to/secure-kubernetes-services-with-ingress-tls-letsencrypt/)
