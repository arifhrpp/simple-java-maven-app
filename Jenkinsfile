node {
    checkout scm
    docker.image('maven:3.9.3-eclipse-temurin-17').inside('-v /root/.m2:/root/.m2') {
        try {
            stage('Build') {
                sh 'mvn -B -DskipTests clean package'
            }
            stage('Test') {
                sh 'mvn test'
            }
        } finally {
            junit 'target/surefire-reports/*.xml'
        }
        stage('Deliver') {
            sh './jenkins/scripts/deliver.sh'
        }
    }
}