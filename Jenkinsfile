pipeline {
    agent any

    // This environment variable helps Jenkins find your K8s config
    environment {
        KUBECONFIG = 'C:\\Users\\nisha\\.kube\\config'
    }

    // This tells Jenkins to use the 'M3' Maven configuration you just set up
    tools {
        maven 'Maven' 
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/NISHA1114/Agile-demo.git'
            }
        }

        stage('Build Maven') {
            steps {
                // This will now work because of the tools block above
                bat 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t springboot-app .'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml --validate=false'
            }
        }
    }
}
