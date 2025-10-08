pipeline {
    agent any
    stages {
        stage('Checkout GIT') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/mhassini/timesheet-devops.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn -version'
                sh 'mvn clean install'
            }
        }
    }
}
