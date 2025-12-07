pipeline {
    agent { label 'ubuntu3' }

    stages {
        stage('Clone Main Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/MUGHEESULHASSAN/testing-_mern_web_app_with_jenkins_pipeline.git'
            }
        }

        stage('Build & Run Main Containers') {
            steps {
                sh 'sudo docker compose down || true'
                sh 'sudo docker compose up -d --build'
            }
        }

        stage('Verify Running Containers') {
            steps {
                sh 'sudo docker ps'
            }
        }

        stage('Show Logs') {
            steps {
                sh 'sudo docker compose logs --tail=50'
            }
        }

        stage('Run Selenium Tests') {
            steps {
   

                
               
                dir('selenium-tests') {
                    sh 'sleep 10'
                 
                    sh 'sudo docker build -t selenium-tests .'

                    
                    sh 'sudo docker run selenium-tests '
                }
            }
        }
    }

    post {
        success {
            echo "✅ CI Build Completed Successfully!"
        }
        failure {
            echo "❌ Build Failed. Check logs."
        }
    }
}
