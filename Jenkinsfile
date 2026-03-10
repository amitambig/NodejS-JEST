pipeline {
    agent {label 'slave-1'}
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/amitambig/NodejS-JEST.git'
            }
        }
        stage('Install dependencies') {
            steps {
                nodejs('node20') {
                    sh 'npm install'
                }
            }
        }
        stage('Test') {
            steps {
                nodejs('node20') {
                    sh 'npm run test'
                }
            }
        }
        stage('Code analysis') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=NodeProj -Dsonar.projectKey=NodeProj \
                    -Dsonar.sources=. -Dsonar.tests=. -Dsonar.test.inclusions=**/*.test.js -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info '''
                }
            }
        }
    }
}
