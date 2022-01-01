// pipeline {
//     agent any
//     stages {
//         stage("Checkout SCM"){
//             steps {
//                 git credentialsId: 'mehedi02', url: 'https://github.com/mehedi02/istio_project.git'
//             }
//         }

//         stage("Build Docker Images"){
//             steps{
//                 dir('sa-frontend') {
//                     sh "docker image build -t mehedi02/frontend:istio . -f build/Dockerfile"
//                 }

//                 dir('sa-logic') {
//                     sh "docker image build -t mehedi02/logic:istio . -f build/Dockerfile"
//                 }

//                 dir('sa-webapp') {
//                     sh "docker image build -t mehedi02/webapp:istio . -f build/Dockerfile"
//                 }
//             }
//         }

//         stage("Push docker images to dockerhub"){
//             steps {
//                 withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHub')]) {
//                     sh "docker login -u mehedi02 -p ${dockerHub}"
//                 }
//                 sh "docker push mehedi02/frontend:istio"
//                 sh "docker push mehedi02/webapp:istio"
//                 sh "docker push mehedi02/logic:istio"
//             }
//         }

//         stage("Deploy app") {
//             steps {
//                     dir("resource-manifests/kube") {
//                         script {
//                             kubernetesDeploy(configs: "sa-frontend-deployment.yaml", kubeconfigId: "mykubernetesconfig")
//                         }
//                         script {
//                             kubernetesDeploy(configs: "sa-logic-deployment.yaml", kubeconfigId: "mykubernetesconfig")
//                         }
//                         script {
//                             kubernetesDeploy(configs: "sa-web-app-deployment.yaml", kubeconfigId: "mykubernetesconfig")
//                         }
//                         script {
//                             kubernetesDeploy(configs: "service-sa-frontend.yaml", kubeconfigId: "mykubernetesconfig")
//                         }
//                         script {
//                             kubernetesDeploy(configs: "service-sa-logic.yaml", kubeconfigId: "mykubernetesconfig")
//                         }
//                         script {
//                             kubernetesDeploy(configs: "service-sa-web-app.yaml", kubeconfigId: "mykubernetesconfig")
//                         }
//                     }
//                     dir("resource-manifests/istio"){
//                         script {
//                             kubernetesDeploy(configs: "http-gateway.yaml", kubeconfigId: "mykubernetesconfig")
//                         }
                        
//                         script {
//                             kubernetesDeploy(configs: "sa-virtualservice-external.yaml", kubeconfigId: "mykubernetesconfig")
//                         }
//                     }
                
                    
//                 }
//             }
//         }
//     }


pipeline {
    agent any
    stages {
        stage("Checkout SCM") {
            steps {
                git credentialsId: 'mehedi02', url: 'https://github.com/mehedi02/istio_project.git'
            }
        }

        // stage("Build Docker Images"){
        //     steps{
        //         dir('sa-frontend') {
        //             sh "docker image build -t mehedi02/frontend:istio ."
        //         }

        //         dir('sa-logic') {
        //             sh "docker image build -t mehedi02/logic:istio ."
        //         }

        //         dir('sa-webapp') {
        //             sh "docker image build -t mehedi02/webapp:istio ."
        //         }
        //     }
        // }

        // stage("Push docker images to dockerhub"){
        //     steps {
        //         withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHub')]) {
        //             sh "docker login -u mehedi02 -p ${dockerHub}"
        //         }
        //         sh "docker push mehedi02/frontend:istio"
        //         sh "docker push mehedi02/webapp:istio"
        //         sh "docker push mehedi02/logic:istio"
        //     }
        // }

        stage ("Deploy App"){
            steps {
                dir("resource-manifests/kube") {
                        script {
                            kubernetesDeploy(configs: "sa-frontend-deployment.yaml", kubeconfigId: "mykubernetesconfig")
                        }
                        script {
                            kubernetesDeploy(configs: "sa-logic-deployment.yaml", kubeconfigId: "mykubernetesconfig")
                        }
                        script {
                            kubernetesDeploy(configs: "sa-web-app-deployment.yaml", kubeconfigId: "mykubernetesconfig")
                        }
                        script {
                            kubernetesDeploy(configs: "service-sa-frontend.yaml", kubeconfigId: "mykubernetesconfig")
                        }
                        script {
                            kubernetesDeploy(configs: "service-sa-logic.yaml", kubeconfigId: "mykubernetesconfig")
                        }
                        script {
                            kubernetesDeploy(configs: "service-sa-web-app.yaml", kubeconfigId: "mykubernetesconfig")
                        }
                    }
                // dir("resource-manifests/istio"){
                //     // script {
                //     //         kubernetesDeploy(configs: "http-gateway.yaml", kubeconfigId: "mykubernetesconfig")
                //     //     }
                        
                //     // script {
                //     //         kubernetesDeploy(configs: "sa-virtualservice-external.yaml", kubeconfigId: "mykubernetesconfig")
                //     //     }

                // }

            }

            steps("istio deployment"){
                dir("resource-manifests/istio"){
                    script {
                        kubernetesDeploy(configs: "http-gateway.yaml", kubeconfigId: "mykubernetesconfig")
                    }
                }
            }
        }
    }
}