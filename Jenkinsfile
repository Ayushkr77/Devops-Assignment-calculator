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
        // create folder for test reports
        bat 'mkdir test-reports'

        // run pytest and generate JUnit XML
        bat 'pytest --junitxml=test-reports/pytest.xml'

        // publish test results
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
