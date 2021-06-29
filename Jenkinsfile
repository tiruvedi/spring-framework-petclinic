pipeline {
    agent any

    stages {
        stage('SCM checkout') {
            steps {
                git 'git@github.com:kuntrapakam/spring-framework-petclinic.git'
            }
        }
        
        stage('Build Stage') {
            steps {
                sh '/opt/maven/bin/mvn clean package'
            }
        }
        
        stage('Storing war into artifactory') {
            steps {
                sh 'mv target/petclinic.war target/petclinic-$BUILD_NUMBER.war'
                sh 'aws s3 cp target/petclinic-$BUILD_NUMBER.war s3://python-rohith-yadav'
            }
        }
        
        stage('Deploy Stage') {
            steps {
                sh 'scp target/petclinic-$BUILD_NUMBER.war root@10.0.15.141:/opt/tomcat/webapps/petclinic.war'
            }
        }
    }
}