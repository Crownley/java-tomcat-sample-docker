  pipeline {
    agent any
    tools { 
        maven 'LocalMaven' 
        jdk 'LocalJK8' 
    }
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                // sh "docker --version"
                // sh "/Applications/Docker.app/Contents/Resources/bin/docker --version"
                sh "docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }

    }
}
