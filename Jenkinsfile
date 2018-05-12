pipeline {
  agent any

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
            def pom = readMavenPom file: 'pom.xml'
            print "Build: " + pom.version
            env.POM_VERSION = pom.version
            sh 'mvn clean test -Dmaven.test.failure.ignore=true'
            junit '**/target/surefire-reports/TEST-*.xml'
            currentBuild.description = "v${pom.version} (${env.branch})"
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

