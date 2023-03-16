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
      steps {
        sh '/usr/share/maven/bin/mvn package'
      }
    }

  }
}