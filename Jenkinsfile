pipeline {
    agent any

    triggers {
        cron('H/3 * * * 1') // Runs every 3 minutes on Mondays
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'git@github.com:karan-handa-clg/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    sh './mvnw clean package'
                }
            }
        }
        
        stage('Run Tests & Generate Coverage Report') {
            steps {
                script {
                    sh './mvnw test jacoco:report'
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}

