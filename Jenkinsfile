pipeline {
    agent any

    stages {    
            stage('Build-$version') {
                steps {
                    dir('spring-boot-package-war') {
                        sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} && mvn clean package"
                        echo 'Building..'
                    }
                }   
            }
            stage('Test-$version') {
                 steps {
                     echo 'Testing..'
                }
            }
            stage('deploy-$version') {
                 steps {
                     echo 'Deploying....'
                 }
              }
            }
        }
    
