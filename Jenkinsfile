pipeline {
    agent { label 'suprith2' }   // ✅ Straight quotes

    tools {
        jdk 'jdk17'
        maven 'Maven3'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/mbgowtham53-star/Java-mini-project.git'
            }
        }
        stage('Build') {
            steps {
                dir('sample-app') {
                sh 'mvn clean package -DskipTests'
            }
        }
       }

        stage('Deploy to Tomcat') {   // ✅ Fixed name + spelling
            steps {
                   sh '''
                WAR_FILE="/home/ubuntu/workspace/sample-app/target/*.war"
                SERVER_IP="172.31.39.195"
                USER_NAME="ubuntu"
                TMP_DIR="/tmp/App"              # ✅ corrected (was /temp/App)
                TOMCAT_DIR="/opt/tomcat/webapps/"

                # Create temp dir if not exists
                ssh $USER_NAME@$SERVER_IP "mkdir -p $TMP_DIR"

                # Copy WAR file
                scp $WAR_FILE $USER_NAME@$SERVER_IP:$TMP_DIR

                # Move WAR into Tomcat
                ssh $USER_NAME@$SERVER_IP "sudo mv $TMP_DIR/*.war $TOMCAT_DIR"
                '''
            }
          }
        }
     }
