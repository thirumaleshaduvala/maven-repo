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
              sh '/usr/share/maven/bin/mvn sonar:sonar'
            }

          }
        }

      }
    }

    stage('deploying artifact') {
      steps {
        sh 'scp /home/jenkins/jenkins-workspace/workspace/newpipe_master/target/studentapp-2.5-SNAPSHOT 172.31.33.73:/usr/share/tomcat/webapps'
      }
    }

  }
}