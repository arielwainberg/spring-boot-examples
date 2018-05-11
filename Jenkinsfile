pipeline {
  agent any

  stages {  
    stage('Build-${env.BUILD_NUMBER}') {
      steps {
        dir('spring-boot-package-war') {
          sh "pwd"
          sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} && mvn clean package"
        //sh "mvn --batch-mode release:update-versions -DdevelopmentVersion=1.2.0-SNAPSHOT"
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
