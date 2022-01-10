pipeline {
  agent {
    node {
      label 'myVM'
    }

  }
  stages {
    stage('Unit Tests') {
      steps {
        sh 'mvn clean test'
        junit(testResults: 'surefire-reports/TEST-*.xml', allowEmptyResults: true)
        jacoco(changeBuildStatus: true, minimumLineCoverage: '55', runAlways: true)
      }
    }

    stage('Build') {
      steps {
        sh 'mvn package -Dmaven.test.skip=true'
        archiveArtifacts(artifacts: '**/*.jar', fingerprint: true, onlyIfSuccessful: true)
      }
    }

  }
}