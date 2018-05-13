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
            sh "mvn -B versions:set -DnewVersion=1.0-SNAPSHOT-${env.BUILD_NUMBER} && mvn clean package"
            version = readMavenPom().getVersion()
            currentBuild.description = "${env.JOB_NAME}-${version}"
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
// project-name-1.0-SNAPSHOT-17.war

//    stage('Version') {
//      steps {
//        dir('spring-boot-package-war') {
//          script {
//            version = readMavenPom().getVersion()
//            currentBuild.description = "${env.JOB_NAME}-${version}"
//          }
//        }
//      }
 
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

