pipeline {
    agent any

    stages {
        stage('Checkout & Build') {
            steps {
                // Récupérer le code depuis Git
                git branch: 'master',
                    url: 'https://github.com/SoulaymaBoukhadra30/-timesheet-devops-soulayma.git'
   }
        }
        stage('Testing maven') {
            steps {
                sh 'mvn -version'
            }
        }
    }
}
