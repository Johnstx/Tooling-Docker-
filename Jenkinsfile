   pipeline {

        environment {
        registry = "johnstx/tooling" 
        registryCredential = 'dockerhub-login' // Jenkins credentials ID for Docker Hub
        image_name = "johnstx/tool"
        Docker_compose_file = "tooling.yaml"
               // BUILD_TAG = 'master-0.0.1'
        }
        
        agent any

        stages {


        stage('Clean Workspace') {
          steps {
                    cleanWs() // Cleans the workspace before running the pipeline
          }
        }


          stage ('Checkout SCM') {
            steps {
              git branch: 'compose' , url : 'https://github.com/Johnstx/Tooling-Docker-.git',   credentialsId: 'github-login'
            }
          }



          // stage('Docker Build image') {
          //   steps {
          //       script {
          //           //  docker.withRegistry( '' ,  'dockerhub-login' ) {
          //                 // Build the Docker image and assign it to dockerImage 
          //                 dockerImage = docker.build("${env.REGISTRY}:${env.BUILD_TAG}")
          //                  }
          //       }
          //   }


           stage('Docker Build image') {
            steps {
                script {
                    //  docker  build using docker-compose
                          sh "docker-compose -f ${Docker_compose_file} build"
                           }
                }
            }

          stage ('tag the docker image') {
            steps {
              script {
                sh "docker image tag ${image_name }:latest ${registry}:cmpse-0.0.1"
                 } 
                }
          }

          stage('Deploy docker image to docker hub') {
            steps {
              script {
                         // log in to docker hub
                      docker.withRegistry ( '', registryCredential) {
                            // dockerImage.push()
                            // push the tagged image
                            sh "docker push ${registry}:cmpse-0.0.1"
                 }
              }
            }
          }
      

        //   stage('Clean up'){
        //      steps{
        //         script {
        //             // sh "docker rmi $registry:latest"
        //             sh "docker rmi ${registry}:feature-0.0.1"
        //      }
        //   }
        // }
 stage('Clean up') {
            steps {
                script {
                    // Clean up local Docker images to save space
                    sh "docker rmi ${image_name }:latest"
                    sh "docker rmi ${registry}:cmpse-0.0.1"
                  }
             }
         }
        }
   }



  
