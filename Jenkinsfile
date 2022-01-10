pipeline {
  agent {
    node {
      label 'myVM'
    }

  }
  stages {
    stage('Unit Tests') {
      post {
        success {
          junit(testResults: '**/target/surefire-reports/TEST-*.xml', allowEmptyResults: true)
          jacoco(changeBuildStatus: true, minimumLineCoverage: '55', runAlways: true)
        }

      }
      steps {
        sh 'mvn clean test'
      }
    }

    stage('Build') {
      post {
        success {
          archiveArtifacts(artifacts: '**/*.jar', fingerprint: true, onlyIfSuccessful: true)
        }

      }
      steps {
        sh 'mvn package -Dmaven.test.skip=true'
      }
    }

  }
}