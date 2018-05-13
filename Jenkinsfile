pipeline {
  agent any

  //environment {
  //    version = readMavenPom().getVersion()
  //}

  stages {  
    stage('Build') {
      steps {
        dir('spring-boot-package-war') {
          script {
            version = readMavenPom().getVersion()
            sh "mvn -B versions:set -DnewVersion=${version}.0.${env.BUILD_NUMBER}-SNAPSHOT && mvn clean package"
          }
        }
        //sh "mvn --batch-mode release:update-versions -DdevelopmentVersion=1.2.0-SNAPSHOT"
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
          script {
            currentBuild.description = "${version}"
          }
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

