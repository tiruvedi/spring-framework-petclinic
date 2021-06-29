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

    stage('store') {
      steps {
        sh '''sh \'mv target/petclinic.war target/petclinic-$BUILD_NUMBER.war\'
                sh \'aws s3 cp target/petclinic-$BUILD_NUMBER.war s3://python-rohith-yadav\''''
      }
    }

    stage('deploy') {
      steps {
        sh 'sh \'scp target/petclinic-$BUILD_NUMBER.war root@10.0.15.141:/opt/tomcat/webapps/petclinic.war\''
      }
    }

  }
}