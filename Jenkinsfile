pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'git@github.com:kuntrapakam/spring-framework-petclinic.git', branch: 'master')
      }
    }

    stage('build') {
      steps {
        sh '/opt/maven/bin/mvn clean package'
      }
    }

    stage('deploy') {
      steps {
        sh 'sh \'scp target/petclinic.war root@10.0.15.141:/opt/tomcat/webapps/\''
      }
    }

  }
}