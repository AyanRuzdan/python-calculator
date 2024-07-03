pipeline {
    agent any
    
    environment {
        REPO_URL = 'https://github.com/AyanRuzdan/python-calculator.git'
        BRANCH_NAME = 'main'
    }
    
    stages {
        stage('Clone repository') {
            steps {
                script {
                    deleteDir()
                    checkout([$class: 'GitSCM',
                              branches: [[name: "refs/heads/${BRANCH_NAME}"]],
                              userRemoteConfigs: [[url: "${REPO_URL}"]]])
                }
            }
        }
        
        stage('List files') {
            steps {
                script {
                    sh "ls -R"
                }
            }
        }
        stage('Setup'){
            steps{
                echo 'Verify python'
                sh 'python3 --version'
                sh 'apt install python3-setuptools'
                sh 'apt install python3-wheel'
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate'
            }
        }
        stage('Run script'){
            steps{
               sh '''
                . venv/bin/activate
                python setup.py sdist bdist_wheel
                '''
            }
        }
    }
}
