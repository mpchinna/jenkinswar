node {
    def tomcatWeb = 'D:\\Auto_deployment\\apache-tomcat-9.0.30\\apache-tomcat-9.0.30\\webapps'
    def tomcatBin = 'D:\\Auto_deployment\\apache-tomcat-9.0.30\\apache-tomcat-9.0.30\\bin'
    def tomcatStatus = ''

    stage('SCM Checkout') {
        git 'https://github.com/mpchinna/jenkinswar.git'
    }

    stage('Compile-Package-create-war-file') {
        // Get maven home path
        def mvnHome = tool name: 'maven-3', type: 'maven'   
        bat "${mvnHome}/bin/mvn package"
    }

    stage('Stop Tomcat Service') {
        steps {
            bat 'net stop "Tomcat9"'
        }
    }

    stage('Deploy to Tomcat') {
        bat "copy target\\JenkinsWar.war \"${tomcatWeb}\\JenkinsWar.war\""
    }

    stage('Start Tomcat Service') {
        steps {
            bat 'net start "Tomcat9"'
        }
    }
}
