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

        stage('Testing Maven') {
            steps {
                // Vérifier la version de Maven pour s'assurer que l'environnement est prêt
                sh 'mvn -version'
            }
        }

        stage('Build Project') {
            steps {
                // Compiler le projet Maven
                sh 'mvn clean install'
            }
        }
    }

    post {
        always {
            echo 'Pipeline terminé.'
        }
        success {
            echo 'Build réussi !'
        }
        failure {
            echo 'Build échoué.'
        }
    }
}
