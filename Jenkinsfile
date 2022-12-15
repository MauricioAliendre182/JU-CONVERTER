pipeline {
    agent any
    stages {
        stage ('Execution') {
             steps {
                 dir('./spring-boot-hello-world') {
                    sh 'chmod +x gradlew'
                    sh 'chmod +x gradle'
                 }
             }
        }
        stage('Assemble') {
            steps {
                dir('./spring-boot-hello-world') {
                    sh './gradlew assemble'
                }
            }
        }
//         stage('Test') {
//              steps {
//                  dir('./spring-boot-hello-world') {
//                      sh './gradlew test'
//                   }
//               }
//          }
        stage('Sonarqube') {
            steps {
                dir('./spring-boot-hello-world') {
                     sh './gradlew sonarqube'
                }
            }
        }

        stage('Upload') {
            steps {
                dir('./spring-boot-hello-world'){
                    sh './gradlew publish --console verbose'
                }
            }
        }
    }
}