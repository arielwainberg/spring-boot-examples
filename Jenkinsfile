pipeline {
  agent any

  stages {  
    stage('Build') {
      steps {
        dir('spring-boot-package-war') {
          sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} && mvn clean package"
        //sh "mvn --batch-mode release:update-versions -DdevelopmentVersion=1.2.0-SNAPSHOT"
        }
      }   
    }

    stage('Test') {
      steps{
        dir('spring-boot-package-war') {
          sh 'mvn test'
        //junit '**/target/surefire-reports/*.xml'     
        }
      }
    }

    stage('deploy') {
      steps {
        dir('spring-boot-package-war') {
          echo 'Deploying....'
        }
      }
    }
  }
}
