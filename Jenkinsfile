pipeline {
  agent any

  stages {  
    stage('Build') {
      steps {
        dir('spring-boot-package-war') {
          sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER}.0-SNAPSHO && mvn clean package"
        //sh "mvn --batch-mode release:update-versions -DdevelopmentVersion=1.2.0-SNAPSHOT"
        }
      }   
    }

    stage('Test') {
      steps{
        dir('spring-boot-package-war') {
         sh 'mvn test'    
        }
      }
    }

    stage('Deploy') {
      steps {
        dir('spring-boot-package-war') {
          echo 'Deploying....'
        }
      }
    }
  }
  post {
    always {
      junit '**/target/surefire-reports/*.xml'
      archiveArtifacts artifacts: '**/target/*.war'
    }
  }
}

