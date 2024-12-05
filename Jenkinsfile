pipeline {
    agent any
    
    stages {
        // Uncomment the below stage if you configured SonarQube
        stage('Run Sonarqube') {
            environment {
                scannerHome = tool 'sonarqubescanner'
            }
            steps {
                withSonarQubeEnv(credentialsId: 'sonarqube', installationName: 'sonarqubeserver') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        stage('Build Docker images on Build Server') {
            steps {
                script {
                    // Execute Ansible playbook on Build Server
                    sh "ssh ubuntu@172.31.42.165 'ansible-playbook /home/ubuntu/build.yaml'"                    // 'ansible-playbook /home/ubuntu/playbook.yaml'"
                
                    
                    }
            }
        }
        
        stage('Deploy Script on Deploy Server') {
            steps {
                script {
                    // Execute deployment playbook on Deploy Server
                    sh "ssh ubuntu@172.31.42.165 'ansible-playbook /home/ubuntu/deploy.yaml'"
                }
            }
        }
    }
}

