pipeline {
  agent any            // or: agent { label 'linux' }

  // triggers block mirrors your Freestyle checkboxes
  triggers {
    // Uncomment what you use:
    // githubPush()
    // pollSCM('H/5 * * * *')
    // cron('H H * * 1-5')
  }

  options {
    // Discard old builds (keep last 30)
    buildDiscarder(logRotator(numToKeepStr: '30'))
    // timestamps() // optional: show timestamps in logs
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/your-username/your-repo.git',
            branch: 'main'
            // , credentialsId: 'your-cred-id'  // if private
      }
    }

    stage('Build') {
      steps {
        echo 'Building...'
        // sh 'mvn clean package'       // or whatever your freestyle ran
        // sh './build.sh'
      }
    }

    stage('Test') {
      steps {
        echo 'Testing...'
        // sh 'pytest -q'
      }
    }
  }

  post {
    always {
      echo 'Pipeline completed.'
      // junit 'reports/**/*.xml'
      // archiveArtifacts artifacts: 'build/**', fingerprint: true
    }
  }
}
