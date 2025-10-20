pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/anastasiiabaranri2024/iic.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('BaranSonar') {
                    sh 'sonar-scanner -Dsonar.projectKey=test-project -Dsonar.sources=.'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
