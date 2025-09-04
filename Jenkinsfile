pipeline {
  agent {
    docker {
      image 'python:3.11-slim'
    }
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Deps') {
      steps {
        sh 'pip install -r requirements.txt'
      }
    }

    stage('Unit Tests') {
      steps {
        sh 'mkdir -p test-reports'
        sh 'pytest --junitxml=test-reports/pytest.xml'
        junit 'test-reports/pytest.xml'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t calc-app .'
      }
    }
  }

  post {
    always {
      echo 'Pipeline finished.'
    }
  }
}
