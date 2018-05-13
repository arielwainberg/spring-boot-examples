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
            name = readMavenPom().getName()
            currentBuild.description = "${env.JOB_NAME}-${version}"
          }
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
          sh "scp target/${name}-${version}.war 172.16.244.141:/var/lib/tomcat7/webapps/${name}.war"
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
