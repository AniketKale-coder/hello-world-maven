pipeline {
    agent any
    
    environment {
        TOMCAT_URL = 'http://174.129.249.22:8080'
        TOMCAT_USER = 'tomcatsc'
        TOMCAT_PASSWORD = 'ani1234'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                script {
                    def mvnHome = tool name: 'Maven', type: 'maven'
                    sh "${mvnHome}/bin/mvn clean package"
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    def warFile = findFiles(glob: '**/target/*.war')[0]
                    sh "curl -u ${TOMCAT_USER}:${TOMCAT_PASSWORD} -T ${warFile} ${TOMCAT_URL}/manager/text/deploy?path=/myapp"
                }
            }
        }
    }
}
