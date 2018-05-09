pipeline {
    agent any

    stages {
        dir('spring-boot-package-war') {
            stage('Build-$version') {
                steps {
                     sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} && mvn clean package"
                     echo 'Building..'
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
    }
