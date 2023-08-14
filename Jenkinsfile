pipeline {
    agent any
    
    environment {
        TOMCAT_URL = 'http://174.129.249.22:8080'
        TOMCAT_USER = 'tomcatsc'
        TOMCAT_PASSWORD = 'ani1234'
        MAVEN_TOOL = 'MyMaven'  // Replace with your Maven installation name
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
                    def mvnHome = tool name: MAVEN_TOOL, type: 'hudson.tasks.Maven$MavenInstallation'
                    sh "${mvnHome}/bin/mvn clean package"
                }
            }
        }
        
        stage('Deploy') {
    steps {
        script {
            def warFile = sh(script: 'find $WORKSPACE -name "*.war" | head -n 1', returnStdout: true).trim()
            sh "curl -u ${TOMCAT_USER}:${TOMCAT_PASSWORD} -T ${warFile} ${TOMCAT_URL}/manager/text/deploy?path=/myapp"
        }
    }
}

    }
}
