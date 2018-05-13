pipeline {
  agent any

  environment {
    VERSION = readMavenPom().getVersion()

  stages {  
    stage('Build') {
      steps {
        dir('spring-boot-package-war') {
          sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER}.0-SNAPSHOT && mvn clean package"
        //sh "mvn --batch-mode release:update-versions -DdevelopmentVersion=1.2.0-SNAPSHOT"
        }
      }   
    }

//    stage('Test') {
//      steps{
//        dir('spring-boot-package-war') {
//         sh 'mvn test'    
//        }
//      }
//    }
    stage('Test') {
      steps {
        dir('spring-boot-package-war') {
           currentBuild.description = "${VERSION}"
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

