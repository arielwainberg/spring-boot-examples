//def version() {
//    def matcher = readFile('pom.xml') =~ '<version>(\\d*)\\.(\\d*)\\.(\\d*)(-SNAPSHOT)*</version>'
//    matcher ? matcher[0] : null
//}
def git
def maven
def scriptVersion='v3.0.0'
fileLoader.withGit('https://git.aurora.skead.no/scm/ao/aurora-pipeline-scripts.git', scriptVersion) {
    git = fileLoader.load('git/git')
    maven = fileLoader.load('maven/maven')
    utilities = fileLoader.load('utilities/utilities')
}

Map<String, Object> props = [:]
deployProperties = "-P sign,build-extras"
props.put('deployProperties', deployProperties)
props.put('mavenSettingsFile', 'github-maven-settings')
props.put('pomPath', 'pom.xml')
props.put('credentialsId', 'github')
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
