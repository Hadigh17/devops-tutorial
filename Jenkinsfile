node {
  stage('Clone repository') {
    checkout scm
  }

  stage('Build image') {
    // Build with plain docker CLI (works on Windows master)
    bat 'docker build -t hadigh17/tutoriall .'
  }

  stage('Test image') {
    // Run something simple inside the Linux container; no workspace mount
    bat 'docker run --rm hadigh17/tutoriall node -v'
    // or: bat 'docker run --rm hadigh17/tutoriall sh -lc "echo Running inside container"'
  }

  stage('Push image') {
    withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DH_USER', passwordVariable: 'DH_PASS')]) {
      bat '''
      docker login -u %DH_USER% -p %DH_PASS%
      docker tag hadigh17/tutoriall:latest hadigh17/tutoriall:%BUILD_NUMBER%
      docker push hadigh17/tutoriall:%BUILD_NUMBER%
      docker push hadigh17/tutoriall:latest
      '''
    }
  }
}
