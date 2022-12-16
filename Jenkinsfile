pipeline {
    agent any
    environment {
        ENV = "QA"
        PROJECT_NAME = "${currentBuild.fullDisplayName}"
    }
    stages {
        stage('QA') {
            when {
                environment(name: "ENV", value: "QA")
            }
            stages {
                stage('This is a level 1 stage QA') { 
                    steps{
                        script{
                            sh "echo stage 1 QA"
                            sh "echo ${env.PROJECT_NAME}"
                        }    
                    }
                }
                stage('This is a level 2 stage QA') { 
                    steps{
                        sh "echo stage 2 QA"
                    }
                }
                stage('This is a level 3 stage QA') { 
                    steps{
                        sh "echo stage 3 QA"
                    }
                }
            }
        }
        stage('Staging') {
            when {
                environment(name: "ENV", value: "Staging")
            }
            stages {
                stage('This is a level 1 stage Staging') { 
                    steps{
                        sh "echo stage 1 Staging"
                    }
                }
                stage('This is a level 2 stage Staging') { 
                    steps{
                        sh "echo stage 2 Staging"
                    }
                }
                stage('This is a level 3 stage Staging') { 
                    steps{
                        sh "echo stage 3 Staging"
                    }
                }
            }
        }
        stage('master') {
            when {
                environment(name: "ENV", value: "master")
            }
            stages {
                stage('This is a level 1 stage master') { 
                    steps{
                        sh "echo stage 1 master"
                    }
                }
                stage('This is a level 2 stage master') { 
                    steps{
                        sh "echo stage 2 master"
                    }
                }
                stage('This is a level 3 stage master') { 
                    steps{
                        sh "echo stage 3 master"
                    }
                }
            }
        }
    }
}
