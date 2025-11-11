pipeline {
    agent any

    stages {
        stage('Hello 1') {
            steps {
                echo 'Hello World 1'
                 //sh 'sudo apt update' // Error
                 sh 'mkdir ex1'
                 sh 'ls -l'
                 //sh 'rm -r ex1'
            }
        }
        stage('Hello 2') {
            steps {
                echo 'Hello World 2'
                sh 'cd ex1'
                sh 'echo "echo Hello World in 2" > 2.txt'
                sh 'ls -l'
            }
        }
        stage('Hello 3') {
            steps {
                echo 'Hello World 3'
                sh 'rm 2.txt'
                sh 'ls -l'
            }
        }
        stage('Hello 4') {
            steps {
                echo 'Hello World 4'
                sh 'rm -r ex1'
                sh 'ls -l'
            }
        }
        stage('Hello 5') {
            steps {
                echo 'Hello World 5'
                sh 'ls -l'
            }
        }
    }
}
