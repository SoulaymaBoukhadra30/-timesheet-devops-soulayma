pipeline {
    agent any

    stages {
        stage('Checkout & Build') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/SoulaymaBoukhadra30/-timesheet-devops-soulayma.git'
            }
        }

        stage('MVN CLEAN') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('MVN COMPILE') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('MVN SONARQUBE') {
            steps {
                sh 'mvn sonar:sonar \
                    -Dsonar.host.url=http://192.168.33.10:9000 \
                    -Dsonar.login=admin \
                    -Dsonar.password=sonar'
            }
        }
    }
}
