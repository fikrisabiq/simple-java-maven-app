node {
    def app

    stage('Checkout') {
        checkout scm
    }

    docker.image('maven:3.9.6-eclipse-temurin-17-alpine').inside('-u 0') {
        stage('Build') {
            sh 'mvn -B -DskipTests clean package'
        }

        stage('Test') {
            try {
                sh 'mvn test'
            } finally {
                junit 'target/surefire-reports/*.xml'
            }
        }
    }

    stage('Deliver') {
        sh './jenkins/scripts/deliver.sh'
    }
}