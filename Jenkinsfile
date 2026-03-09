pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t jiyak/sum-product_fx:latest .'
                }
            }
        }

        stage('Start Containers') {
            steps {
                script {
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Verify Database') {
            steps {
                script {
                    sh '''
                    docker exec -i calculator-db mariadb -uroot -pTest12 -e "USE calc_data; SHOW TABLES;"
                    '''
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    sh 'docker-compose down'
                }
            }
        }
    }
}