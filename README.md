# NTI-jenkins
# Jenkins Pipeline
This document shows you the steps of the Jenkins pipeline for building and deploying Dockerized applications to Kubernetes and minikube cluster.

# Pipeline Stages:
1- **Build Docker Image:** Build a Docker image for the application.

2- **Push Docker Image To DockerHub:** Push the Docker image to DockerHub.

3- **Edit new image in deployment.yaml file:** Edit new image in deployment.yaml file.

4- **Deploy the image to kubernetes:** Deploy the image to kubernetes minikube cluster.

scroll down to see pipeline stages Code.

![WhatsApp Image 2024-04-24 at 23 26 00_73170ac9](https://github.com/ramy282/NTI-jenkins/assets/60857262/565d6db6-9a56-4dc5-a77a-39a3dbdf4ee0)

![WhatsApp Image 2024-04-24 at 23 22 27_45915c85](https://github.com/ramy282/NTI-jenkins/assets/60857262/c2bda2c2-3a7b-4e48-8492-3d1b23f3d9b8)

![WhatsApp Image 2024-04-24 at 23 22 44_f4107bd7](https://github.com/ramy282/NTI-jenkins/assets/60857262/dbb886d3-048c-4be9-b941-4f24de0ab9c7)

![WhatsApp Image 2024-04-24 at 23 24 25_805787d4](https://github.com/ramy282/NTI-jenkins/assets/60857262/86bbeaeb-e033-40ab-8a0c-737ec8af6ee3)


### 1- Build Docker Image:

```
 stage('Build Docker image from Dockerfile in GitHub') {
            steps {
                script {
                 	
                 		buildDockerImage("${imageName}")
                      
                }
            }
        }
```

# 2- Push Docker Image To DockerHub:

```
stage('Push image to Docker hub') {
            steps {
                script {
                 	
                 		pushDockerImage("${dockerHubCredentialsID}", "${imageName}")
                      
                }
            }
        }
```

# 3- Edit new image in deployment.yaml file:

```
stage('Edit new image in deployment.yaml file') {
            steps {
                script { 
                	dir('k8s') {
				        editNewImage("${imageName}")
                    	}
                }
            }
        }
```

# 4- Deploy the image to kubernetes:

```
stage('Deploy on k8s Cluster') {
            steps {
                script { 
                	dir('k8s') {
				         deployOnKubernetes("${k8sCredentialsID}")
                    }
                }
            }
        }
```
# Some tips to avoid coman errrors during building:

1- Make sure that the minikube and the docker image on he same network.

2- Make sure that you defined the library's name at the top of jenkines file for example : #@Library('Jenkins-Shared-Library')_.

3- Install Minikube and Kubernetes inside the container.
