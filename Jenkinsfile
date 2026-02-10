pipeline {
    agent any

    stages {
        stage('Checkout GIT') {
            steps {
                echo 'Pulling...'
                git branch: 'master',
                    url: 'https://github.com/SoulaymaBoukhadra30/-timesheet-devops-soulayma.git'
            }
        }

        stage('Testing Maven') {
            steps {
                echo 'Checking Maven version...'
                sh 'mvn -version'
            }
        }

        stage('Build Maven') {
            steps {
                echo 'Building project...'
                sh 'mvn clean install'
            }
        }
    }
}
