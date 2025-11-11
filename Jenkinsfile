pipeline {
    agent any
    options {
        timestamps()
    }
    stages {
        stage('Hello 1') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo 'Hello World 1'
                 //sh 'sudo apt update' // Error
                 sh 'mkdir ex1'
                 sh 'ls -l'
                 //sh 'rm -r ex1'
                 echo "Hello ${params.PERSON}"
            }
        }
        stage('Hello 2') {
            input {
                message "Should we continue?"
                //ok "Yes, we should."
                //submitter "alice,bob"
                parameters {
                text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
            	}            
            }
            steps {
                echo 'Hello World 2'
                sh 'cd ex1'
                sh 'echo "echo Hello World in 2" > 2.txt'
                sh 'ls -l'
                echo "Biography: ${params.BIOGRAPHY}"
            }
        }
        stage('Hello 3') {
            input {
                message "Should we continue?"
                //ok "Yes, we should."
                //submitter "alice,bob"
                parameters {
                booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
            	}            
            }
            steps {
                echo 'Hello World 3'
                sh 'rm 2.txt'
                sh 'ls -l'
                echo "Toggle: ${params.TOGGLE}"
            }
        }
        stage('Hello 4') {
            input {
                message "Should we continue?"
                //ok "Yes, we should."
                //submitter "alice,bob"
                parameters {
                choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
            	}            
            }            
            steps {
                echo 'Hello World 4'
                sh 'rm -r ex1'
                sh 'ls -l'
                echo "Choice: ${params.CHOICE}"
            }
        }
        stage('Hello 5') {
            input {
                message "Should we continue?"
                //ok "Yes, we should."
                //submitter "alice,bob"
                parameters {
                password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
            	}            
            }            
            steps {
                echo 'Hello World 5'
                sh 'ls -l'
                echo "Password: ${params.PASSWORD}"
            }
        }
    }
}
