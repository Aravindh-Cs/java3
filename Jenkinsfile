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

        stage('Stop Tomcat') {
            steps {
                echo "Stopping Tomcat..."
                bat """
                    set CATALINA_HOME=${TOMCAT_HOME}
                    "${TOMCAT_HOME}\\bin\\shutdown.bat"
                """
                echo "Waiting 5 seconds..."
                bat "timeout /t 5 /nobreak"
            }
        }

        stage('Deploy WAR') {
            steps {
                echo "Deploying WAR..."
                bat """
                    copy /Y target\\${WAR_NAME} ${TOMCAT_HOME}\\webapps\\
                """
            }
        }

        stage('Start Tomcat') {
            steps {
                echo "Starting Tomcat..."
                bat """
                    set CATALINA_HOME=${TOMCAT_HOME}
                    "${TOMCAT_HOME}\\bin\\startup.bat"
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
