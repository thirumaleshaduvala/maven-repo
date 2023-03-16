pipeline {
  agent {
    node {
      label 'slave-1'
    }

  }
  stages {
    stage('scm') {
      steps {
        git(url: 'https://github.com/manuravipati/maven-repo.git', branch: 'master', credentialsId: 'git-token')
      }
    }

    stage('build') {
      parallel {
        stage('build') {
          steps {
            sh '/usr/share/maven/bin/mvn package'
          }
        }

        stage('QA') {
          steps {
            withSonarQubeEnv(installationName: 'sonar Qube', credentialsId: 'sonarToken') {
              sh '/usr/share/maven/mvn sonar:sonar'
            }

          }
        }

      }
    }

  }
}