node {
    stage('Checkout') {
        checkout scm
    }

    docker.image('maven:3-eclipse-temurin-21-alpine').inside('-u 0') {
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
        sh 'chmod +x ./jenkins/scripts/deliver.sh && ./jenkins/scripts/deliver.sh'
    }
}