pipeline {
    agent any

    tools {
        jdk 'jdk17'      // must match Manage Jenkins → Tools name
        maven 'maven3'   // must match Tools name
    }

    stages {
        stage('Checkout Code') {
            steps {
                https://github.com/pratheekshaprakash0299-bit/jenkins_pipeline.git
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -B clean package -DskipTests'
            }
        }
    }
}
