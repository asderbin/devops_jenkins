pipeline {
    agent none
    stages {
        stage ('git clone dockerfile for builder') {
            agent {label 'builder'}
            steps {
                echo 'stage 1: git clone dockerfile for builder'
                sh 'rm -rf /var/jenkins/workspace/Homework_Lesson11/Lesson11_Dockerfile-for-builder'
                sh 'git clone https://github.com/asderbin/Lesson11_Dockerfile-for-builder.git'
            }
        }
        stage ('build docker image') {
            agent {label 'builder'}
            steps {
                echo 'stage 2: build docker image'
                sh 'cd /var/jenkins/workspace/Homework_Lesson11/Lesson11_Dockerfile-for-builder/'
                sh 'ls'
                sh 'docker build -t boxfuse-in-docker-v01 /var/jenkins/workspace/Homework_Lesson11/Lesson11_Dockerfile-for-builder/'
            }
        }
        stage ('push docker image to nexus') {
            agent {label 'builder'}
            steps {
                echo 'stage 3: push docker image to nexus'
                sh 'docker tag boxfuse-in-docker-v01 94.139.247.22:8085/boxfuse-in-docker-v01:1.0.0'
                sh 'docker push 94.139.247.22:8085/boxfuse-in-docker-v01:1.0.0'
            }
        }
        stage ('git clone dockerfile for prod') {
            agent {label 'prod'}
            steps {
                echo 'stage 4: git clone dockerfile for prod'
                sh 'rm -rf /var/jenkins/workspace/Homework_Lesson11/Lesson11_Dockerfile-for-prod'
                sh 'git clone https://github.com/asderbin/Lesson11_Dockerfile-for-prod.git'
            }
        }
        stage ('deploy java application') {
            agent {label 'prod'}
            steps {
                echo 'stage 5: deploy java application'
                sh 'cd /var/jenkins/workspace/Homework_Lesson11/Lesson11_Dockerfile-for-prod/'
                sh 'ls'
                sh 'docker build -t boxfuse-in-docker-v01-prod /var/jenkins/workspace/Homework_Lesson11/Lesson11_Dockerfile-for-prod/'
                sh 'docker run -d -p 8080:8080 boxfuse-in-docker-v01-prod'
            }
        }
    }
}