node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("hadigh17/tutoriall")
    }

    stage('Test image') {
        // Replace app.inside with a plain docker run to avoid C:/ path issue
        bat 'docker run --rm hadigh17/tutoriall echo "Tests passed"'
    }

    stage('Push image') {
    withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
        bat """
            docker login -u %DOCKER_USER% -p %DOCKER_PASS%
            docker tag hadigh17/tutoriall hadigh17/tutoriall:${env.BUILD_NUMBER}
            docker tag hadigh17/tutoriall hadigh17/tutoriall:latest
            docker push hadigh17/tutoriall:${env.BUILD_NUMBER}
            docker push hadigh17/tutoriall:latest
        """
        }
    }
}
