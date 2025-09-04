pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Deps') {
      steps {
        bat 'pip install -r requirements.txt'
      }
    }

    stage('Unit Tests') {
        steps {
            bat 'mkdir test-reports'
            bat 'set PYTHONPATH=%CD% && pytest --junitxml=test-reports/pytest.xml'
            junit 'test-reports/pytest.xml'
        }
    }


    stage('Build Docker Image') {
      steps {
        bat 'docker build -t calc-app .'
      }
    }
  }

  post {
    always {
      echo 'Pipeline finished.'
    }
  }
}
