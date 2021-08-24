pipeline {
    agent any

    stages {
        stage('SCM checkout') {
            steps {
                git 'https://github.com/kuntrapakam/spring-framework-petclinic.git'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "mvn clean package sonar:sonar"
                }
            }
        }
        stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
            post {
                always {
                    junit '**/*.xml'
                }
            }
        }
        stage('nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'spring-framework-petclinic', classifier: '', file: 'target/petclinic.war', type: 'war']], credentialsId: 'nexus', groupId: 'org.springframework.samples', nexusUrl: '54.224.198.41:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'chocolate', version: '5.3.8'
            }
        }
        stage('deploy') {
            steps{
                sh 'sudo scp target/petclinic.war /root/tomcat/webapps'
            }
        }
    }
}