pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'hello_world'
    }
    stages {
        stage('checkout') {
            steps {
                git(url: 'https://github.com/shraddhavyas1/jenkins/', branch: 'main')
            }
        }

        stage('Build') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'python -m unittest test_hello_world.py'
            }
        }

        stage('pack') {
            steps {
                sh '''cp -r * ${WORKSPACE}/build
cp Dockerfile ${WORKSPACE}/build'''
            }
        }

        stage('deploy') {
            steps {
                dir("${WORKSPACE}/") {
                    sh "docker build -t $DOCKER_IMAGE ."
                }
                sh "docker run -d -p 8080:8080 $DOCKER_IMAGE"
            }
        }
    }
}
