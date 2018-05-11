//def version() {
//    def matcher = readFile('pom.xml') =~ '<version>(\\d*)\\.(\\d*)\\.(\\d*)(-SNAPSHOT)*</version>'
//    matcher ? matcher[0] : null
//}

pipeline {
  agent any
  
  stages {
    stage('Bump version') {
      origPom = readMavenPom file: 'pom.xml'
      maven.run("no.skatteetaten.aurora.maven.plugins:aurora-cd:${origPom.version}:suggest-version versions:set -DgenerateBackupPoms=false", props)
      // Read pom.xml
      pom = readMavenPom file: 'pom.xml'

      // Set build name
      currentBuild.displayName = "$pom.version (${currentBuild.number})"

      if (!pom.version.endsWith("-SNAPSHOT")) {
          git.tagIfNotExists(props.credentialsId, "v$pom.version")
      }
    }

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
