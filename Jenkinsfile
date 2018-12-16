pipeline {
    agent any

    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker login -u="$DOCKER_USER" -p="$DOCKER_PASS"'
                sh 'mvn -q package'
                sh 'docker build -t pet-clinic .'
                sh 'docker tag pet-clinic $DOCKER_USER/pet-clinic:latest'
                sh 'docker push $DOCKER_USER/pet-clinic:latest'
            }
        }
       
    }
}
