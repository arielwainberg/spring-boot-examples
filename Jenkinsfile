def version() {
    def matcher = readFile('pom.xml') =~ '<version>(\\d*)\\.(\\d*)\\.(\\d*)(-SNAPSHOT)*</version>'
    matcher ? matcher[0] : null
}

pipeline {
  agent any
  
  stages {  
    stage('Build-{$matcher}') {
      steps {
        dir('spring-boot-package-war') {
          sh "pwd"
          sh "mvn -B versions:set -DnewVersion=${env.BUILD_NUMBER} && mvn clean package"
        //sh "mvn --batch-mode release:update-versions -DdevelopmentVersion=1.2.0-SNAPSHOT"
        }
      }   
    }
    stage('Test-$matcher') {
      steps {
        echo 'Testing..'
      }
    }
    stage('deploy-$matcher') {
      steps {
        echo 'Deploying....'
      }
    }
  }
}
