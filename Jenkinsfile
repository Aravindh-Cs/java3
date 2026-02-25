pipeline {
    agent any

    tools {
        jdk 'JDK'        // Replace with your Jenkins JDK tool name
        maven 'MAVEN'    // Replace with your Jenkins Maven tool name
    }

    environment {
        TOMCAT_HOME = 'C:\\appache\\apache-tomcat-9.0.115-windows-x64\\apache-tomcat-9.0.115'
        WAR_NAME = 'java.war'
    }

    stages {

        stage('Build WAR') {
            steps {
                echo "Building WAR..."
                bat 'mvn clean package'
            }
        }

        stage('Deploy WAR') {
            steps {
                echo "Deploying WAR to Tomcat..."
                bat """
                    copy /Y target\\${WAR_NAME} ${TOMCAT_HOME}\\webapps\\
                """
            }
        }
    }

    post {
        success {
            echo "Deployment complete! Access your app at http://localhost:8081/java/index.jsp"
        }
        failure {
            echo "Deployment failed! Check WAR name, paths, or Tomcat logs."
        }
    }
}
