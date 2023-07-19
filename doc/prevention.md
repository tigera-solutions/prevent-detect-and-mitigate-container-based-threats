# Prevention


## Image Assurance

Detect vulnerabilities in container images at build and runtime.

Before deploying our application, let's [scan the images for vulnerabilities](https://docs.calicocloud.io/image-assurance/scan-image-registries) using the CLI.

```
docker pull quay.io/jsabo/log4shell-vulnerable-app:latest
tigera-scanner scan quay.io/jsabo/log4shell-vulnerable-app:latest
```

Explore the image scan results in Calico Cloud.

![cc](img/cc-scan-result.png)

The command line interface (CLI) based scanner can easily be integrated into a developer's workflow and continuous integration/continuous delivery (CI/CD) pipelines.  For example, we have integrated the CLI based scanner into our development process using [Github Actions workflows](https://github.com/tigera-solutions/prevent-detect-and-mitigate-container-based-threats/blob/main/.github/workflows/run-tigera-scanner.yaml).

To view the results of the Tigera container scan, click on the workflow status badge below.

[![Calico Cloud Container Scan Results](https://github.com/tigera-solutions/detect-and-mitigate-container-based-threats/actions/workflows/run-tigera-scanner.yaml/badge.svg)](https://github.com/tigera-solutions/detect-and-mitigate-container-based-threats/actions/workflows/run-tigera-scanner.yaml)


## Admission Controller

Use policy to prevent vulnerable container images from being deployed.

Before [deploying the admission controller](https://docs.calicocloud.io/image-assurance/install-the-admission-controller), we have to create some certificates to secure the communication between the controller and the Kubernetes api.  Once we have the certs we can add them to the admission controller deployment and apply them to the cluster.  

```
curl https://installer.calicocloud.io/manifests/v3.16.1-11/manifests/generate-open-ssl-key-cert-pair.sh | bash
sed -i '' "s/BASE64_CERTIFICATE/$(base64 < admission_controller_cert.pem)/g" workshop/iaac/tigera-image-assurance-admission-controller-deploy.yaml
sed -i '' "s/BASE64_KEY/$(base64 < admission_controller_key.pem)/g" workshop/iaac/tigera-image-assurance-admission-controller-deploy.yaml
kubectl create -f workshop/iaac
```

Let's deploy the workshop applications.

```
kubectl apply -f apps
```

Notice the following error in the output.

```
Error from server (Action 'Reject' enforced by ContainerPolicy reject-failed rule index 1): error when creating "apps/java-app.yaml": admission webhook "image-assurance.tigera.io" denied the request: Action 'Reject' enforced by ContainerPolicy reject-failed rule index 1
```

The deployment of the `java-app` will fail because the Admission Controller policy is preventing the deployment of vulnerable workloads.


## Vulnerability Management

Our admission controller should prevent running applications with CVSS scores above 7.  These are the vulnerabilities with `critical` and `high` CVSS scores.  We want to override the policy that prevents the deployment of the `java-app` due to critical vulnerabilities so that we can access it.

Select the image and choose all the Critical and High CVEs.  Click on Bulk Edit and add an exception. 

![cc](img/cc-add-exception.png)

After creating exceptions for the vulnerabilities, you should now be able to deploy the vulnerable 'java-app' workload.

```
kubectl label namespaces java-app tigera-admission-controller-
kubectl apply -f apps/java-app.yaml
```


[Next -> Module 5](detection.md)
