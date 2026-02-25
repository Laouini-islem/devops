pipeline {
    agent any
    
    stages {
        stage('GIT') {
            steps {
                // Récupération du code depuis Git
                git 'https://github.com/Laouini-islem/devops'
            }
        }
        
        stage('MAVEN Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        
        stage('SONARQUBE') {
            environment {
                SONAR_HOST_URL = 'http://192.168.33.10:9000/'
                SONAR_AUTH_TOKEN = credentials('sonarqube')  // ID du credential créé
            }
            steps {
                sh '''
                    mvn sonar:sonar \
                    -Dsonar.projectKey=devops_git \
                    -Dsonar.host.url=${SONAR_HOST_URL} \
                    -Dsonar.token=${SONAR_AUTH_TOKEN}
                '''
            }
        }
    }
}
