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
        stage ('SCM'){
            git 'https://github.com/foo/bar.git'
        }
        stage('Sonarqube') {
            steps {
                dir('./spring-boot-hello-world') {
                     withSonarQubeEnv() { // Will pick the global server connection you have configured
                          sh './gradlew sonarqube'
                      }
                }
            }
        }
    }
}