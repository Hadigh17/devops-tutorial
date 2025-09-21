node {
    def app

    stage('Clone repository') {
        /* Clone the repository into the workspace */
        checkout scm
    }

    stage('Build image') {
        /* Build the Docker image */
        app = docker.build("hadigh17/tutoriall")
    }

    stage('Test image') {
        /* Run a simple test inside the container */
        app.inside('-w /c/Users/hadig/.jenkins/workspace/edureka-pipeline') {
            sh 'echo Running inside container'
        }
    }

    stage('Push image') {
        /* Push the image to Docker Hub with tags */
        docker.withRegistry('https://index.docker.io/v1/', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
