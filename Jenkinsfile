
   pipeline {


        environment {
        registry = "johnstx/tooling" 
        registryCredential = 'dockerHub' // Jenkins credentials ID for Docker Hub
        TAG = 'latest'
        }

    agent any

    stages {
          stage ('Initial cleanup') {
            steps {
                    dir("${WORKSPACE}") {
                  deleteDir ()
                    }
            }
          }


          stage ('Checkout SCM') {
            steps {
              git branch: 'feature' , url : 'https://github.com/Johnstx/Tooling-Docker-.git', credentialsId: 'GitHub-login'
            }
          }

          stage('Docker Build Image') {
               steps {
                      script {
                          // Build the Docker image and assign it to dockerImage
                          dockerImage = docker.build("${registry}:latest")
                            }
                      }
              }
          }



          // // stage('Docker Build image') {
          // //   steps {
          // //       script {
          // //            docker.withRegistry( '' ,  'dockerHub' ) {
          // //                 // Build the Docker image and assign it to dockerImage 
          // //                 dockerImage = docker.build("${registry}:latest")
          // //                  }
          // //       }
          // //   }
          // // }

          // stage ('tag the docker image') {
          //   steps {
          //       sh 'docker image tag ${registry}:latest ${registry}:feature-0.0.1'
          //       }
          // }

          // stage('Deploy docker image to docker hub') {
          //   steps {
          //     script {
          //                // log in to docker hub
          //             docker.withRegistry ( '', registryCredential) {
          //                   dockerImage.push()
          //        }
          //     }

          //   }
          // }

          // stage('Remove unsused images'){
          //    steps{
          //           sh "docker rmi $registry:latest"
          //           sh "docker rmi ${registry}:feature-0.0.1"
          // }
      //   }

      // }



    }
  
