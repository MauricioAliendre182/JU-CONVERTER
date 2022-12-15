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
        stage('Test') {
             steps {
                 dir('./spring-boot-hello-world') {
                     sh './gradlew test'
                  }
              }
         }
        stage('Sonarqube') {
            steps {
                dir('./spring-boot-hello-world') {
                     sh './gradlew sonarqube'
                }
            }
        }
//         stage('Report') {
//             steps {
//                 //allure includeProperties: false, jdk: '', results: [[path: 'allure-report']]
//               dir('./spring-boot-hello-world') {
//                 script {
//                     allure([
//                             includeProperties: false,
//                             jdk: '',
//                             properties: [],
//                             reportBuildPolicy: 'ALWAYS',
//                             results: [[path: 'allure-report']]
//                     ])
//                  }
//               }
//            }
//         }
        stage("Quality Gate") {
            steps {
              dir('./spring-boot-hello-world'){
                timeout(time: 2, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
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