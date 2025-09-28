pipeline{
   agent none
      tools {
        jdk 'jdk17'
        maven 'maven3'
    }
      stages {
           stage ('checkout code') {
      
           agent {label 'c-project'}
                steps { 
                     git branch: 'main',
                     url: 'https://github.com/Suprith25/Jenkins-mini-project.git'
                     
                        
}
}
       stage('Build') {
            steps {
                dir('sample-app') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }
}
