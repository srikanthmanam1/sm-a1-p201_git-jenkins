pipeline {
    agent any
    // ----------------- options --------------
    options {
	// ----------------- Time Stamp --------------
        timestamps()

	// -------- Day and number of builds to keep the build ------------
        buildDiscarder(logRotator(daysToKeepStr: '14', numToKeepStr: '10'))
    }
    // --------------- Parameters ----------------
    parameters {
    	string(name: 'BRANCH', defaultValue: 'main', description: 'Git branch to build')
    }
    // -------- Environment Variables ------------
    environment {
        APP_ENV = 'staging'
        AWS_CREDENTIALS = credentials('aws-creds-id')
	IMAGE_NAME = "my-app"
        GIT_COMMIT_SHORT = sh(script: 'git rev-parse --short HEAD', returnStdout: true).trim()
        DEPLOY_ENV = 'production'
    }

    stages {

    	// -------- Git Repo Check ------------
    	// ----- Tells Jenkins to check out source code from ----
    	// ---- SCM Source Control Management system configured in the job (e.g., Git).
	stage('Checkout') {
            steps {
                checkout scm
            }

        stage('Hello 1') {
            steps {
                echo 'Hello World 1'
                 //sh 'sudo apt update' // Error
                 sh 'mkdir ex1'
                 sh 'ls -l'
                 //sh 'rm -r ex1'
    		// -------- Environment Variables ------------
		echo "Building ${IMAGE_NAME}:${GIT_COMMIT_SHORT}"
                echo "Deploying to ${env.DEPLOY_ENV}"
            }
        }
        stage('Hello 2') {
            steps {
                echo 'Hello World 2'
                sh 'cd ex1'
                sh 'echo "echo Hello World in 2" > 2.txt'
                sh 'ls -l'
	        // ---- timeout: time for timeout (minutes, seconds, hours, etc.).-------
		// ---- Specify how long code block can runs, exit after timeout---------
		timeout(time: 30, unit: 'MINUTES') {
		    sh './ex2.sh'
		}
            }
        }
        stage('Hello 3') {
            steps {
                echo 'Hello World 3'
                sh 'rm 2.txt'
                sh 'ls -l'
                // ---- retry(3): max 3 times or success.-------    
		retry(3) {
		    sh './ex3.sh'
		}
            }
        }
        stage('Hello 4') {
            steps {
                echo 'Hello World 4'
                sh 'rm -r ex1'
                sh 'ls -l'
    		// --------------- Parameters ----------------    
		echo "Building branch ${params.BRANCH}"
            }
        }
        stage('Hello 5') {
            steps {
                echo 'Hello World 5'
                sh 'ls -l'
            }
        }
    }
    // ------- Ending message of pipeline build ------
    post {
        success {
            echo 'Build succeeded!'
	    echo "Build and deployment succeeded for ${IMAGE_NAME}:${GIT_COMMIT_SHORT}"
        }
        failure {
            echo 'Build failed!'
            echo "Build failed for ${IMAGE_NAME}:${GIT_COMMIT_SHORT}"
        }
	// ----- Always cleans up the workspace ------------
	// ----- delete files from workspace directory -----
	always {
            cleanWs()
        }
    }
}
