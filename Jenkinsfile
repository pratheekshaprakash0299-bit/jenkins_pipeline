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

        stage('Upload to JFrog') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'jfrog-creds',
                                                 usernameVariable: 'JFROG_USER',
                                                 passwordVariable: 'JFROG_PASS')]) {
                    sh '''
                        echo "Uploading WAR to JFrog..."
                        WAR_FILE=$(ls sample-app/target/*.war)
                        curl -u $JFROG_USER:$JFROG_PASS -T $WAR_FILE \
                        "https://trialxl53ee.jfrog.io/artifactory/DevOps/${JOB_NAME}-${BUILD_NUMBER}-sample.war"
                    '''
                }
            }
        }
    }
}
