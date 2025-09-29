pipeline {
    agent any

    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    environment {
        JFROG_USER = "your-jfrog-username"
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

        stage('Upload WAR to JFrog') {
            steps {
                withCredentials([string(credentialsId: 'jfrog-creds', variable: 'JFROG_TOKEN')]) {
                    sh '''
                        echo "Uploading WAR to JFrog..."
                        WAR_FILE=$(ls sample-app/target/*.war)
                        curl -v -L -u $JFROG_USER:$JFROG_TOKEN -T $WAR_FILE \
                        "https://trialxl53ee.jfrog.io/artifactory/DevOps/${JOB_NAME}-${BUILD_NUMBER}-sample.war"
                    '''
                }
            }
        }
    }
}
