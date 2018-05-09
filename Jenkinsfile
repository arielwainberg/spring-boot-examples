pipeline {
  agent any

  stages {  
    stage('Build-$version') {
      steps {
        dir('spring-boot-package-war') {
          sh "pwd"
          sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} && mvn clean package"
        }
      }   
    }
}
