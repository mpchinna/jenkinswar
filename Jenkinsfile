pipeline {
    agent any
    
    environment {
        // Define environment variables here if needed
        tomcatWeb = 'D:\\Auto_deployment\\apache-tomcat-9.0.30\\apache-tomcat-9.0.30\\webapps'
        tomcatBin = 'D:\\Auto_deployment\\apache-tomcat-9.0.30\\apache-tomcat-9.0.30\\bin'
    }
    
    stages {
        stage('SCM Checkout') {
            steps {
                git 'https://github.com/mpchinna/jenkinswar.git'
            }
        }
        
        stage('Compile-Package-create-war-file') {
            steps {
                // Get Maven home path
                def mvnHome = tool name: 'maven-3', type: 'maven'   
                bat "${mvnHome}/bin/mvn package"
            }
        }
        
        stage('Stop Tomcat Service') {
            steps {
                bat 'net stop "Tomcat9"'
            }
        }
        
        stage('Deploy to Tomcat') {
            steps {
                bat "copy target\\JenkinsWar.war \"${tomcatWeb}\\JenkinsWar.war\""
            }
        }
        
        stage('Start Tomcat Service') {
            steps {
                bat 'net start "Tomcat9"'
            }
        }
    }
}
