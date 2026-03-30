pipeline {
    agent any

    stages {

        // ── Slide 20 : Récupération depuis Git ──────────────────
        stage('GIT') {
            steps {
                echo "Getting Project from Git"
                git branch: 'master',
                    url: 'https://github.com/SoulaymaBoukhadra30/-timesheet-devops-soulayma.git'
            }
        }

        // ── Slide 21 : Maven Clean ───────────────────────────────
        stage('MVN CLEAN') {
            steps {
                sh 'mvn clean'
            }
        }

        // ── Slide 21 : Maven Compile ─────────────────────────────
        stage('MVN COMPILE') {
            steps {
                sh 'mvn compile'
            }
        }

        // ── Slide 22 : Analyse SonarQube ─────────────────────────
        stage('MVN SONARQUBE') {
            steps {
                sh '''
                    mvn sonar:sonar \
                        -Dsonar.host.url=http://192.168.33.10:9000 \
                        -Dsonar.login=admin \
                        -Dsonar.password=sousou
                '''
            }
        }

        // ── Bonus : Package Maven (pour Docker) ──────────────────
        stage('MVN PACKAGE') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }

        // ── Partie Docker ─────────────────────────────────────────
        stage('DOCKER BUILD') {
            steps {
                sh 'docker build -t timesheet-app:latest .'
            }
        }

        stage('DOCKER RUN') {
            steps {
                sh '''
                    docker stop timesheet-app || true
                    docker rm   timesheet-app || true
                    docker run -d \
                        --name timesheet-app \
                        -p 8082:8082 \
                        timesheet-app:latest
                '''
            }
        }
    }

    post {
        success {
            echo " Pipeline terminé — voir les résultats sur http://192.168.33.10:9000"
        }
        failure {
            echo " Pipeline échoué"
        }
    }
}
