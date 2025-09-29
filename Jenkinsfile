pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Suprith25/Java-mini-project.git'
            }
        }

        stage('Build') {
            steps {
                dir('sample-app') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Upload to JFrog') {
            steps {
                withCredentials([string(credentialsId: 'jfrog_token', variable: 'JFROG_TOKEN')]) {
                    sh '''
                        echo "Uploading WAR to JFrog using token..."
                        WAR_FILE=$(ls sample-app/target/*.war)
                        curl -H "Authorization: Bearer $JFROG_TOKEN" -T $WAR_FILE \
                        "https://trialxl53ee.jfrog.io/artifactory/qwertyuiop/${JOB_NAME}-${BUILD_NUMBER}-sample.war"
                    '''
                }
            }
        }
    }
}
