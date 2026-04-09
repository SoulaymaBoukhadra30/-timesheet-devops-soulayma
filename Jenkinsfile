pipeline {
    agent any
    stages {
        stage('GIT') {
            steps {
                echo "Getting Project from Git"
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
                sh '''
                    mvn sonar:sonar \
                        -Dsonar.host.url=http://192.168.33.10:9000 \
                        -Dsonar.login=admin \
                        -Dsonar.password=sousou
                '''
            }
        }
        stage('MVN PACKAGE') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }
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
        stage('DOCKER PUSH') {
            steps {
                sh '''
                    docker tag timesheet-app:latest SoulaymaBoukhadra30/timesheet-app:latest
                    docker push SoulaymaBoukhadra30/timesheet-app:latest
                '''
            }
        }
        stage('KUBERNETES DEPLOY') {
            steps {
                sh '''
                    kubectl apply -f k8s/pv-sql.yaml -n devops
                    kubectl apply -f k8s/pvc-sql.yaml -n devops
                    kubectl apply -f k8s/deploy-sql.yaml -n devops
                    kubectl apply -f k8s/service-sql.yaml -n devops
                    kubectl apply -f k8s/configmap-spring.yaml -n devops
                    kubectl apply -f k8s/secret-spring.yaml -n devops
                    kubectl apply -f k8s/deploy-spring.yaml -n devops
                    kubectl apply -f k8s/service-spring.yaml -n devops
                '''
            }
        }
    }
    post {
        success {
            echo "Pipeline terminé !"
        }
        failure {
            echo "Pipeline échoué"
        }
    }
}
