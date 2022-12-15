pipeline{
    agent any
    stages{
        stage("QA"){
            when {
                branch 'QA'
            }
            stage("SCM"){
                steps{
                    checkout([$class: 'GitSCM', 
			            branches: [[name: '*/QA']], 
			            extensions: [], 
			            userRemoteConfigs: [[ 
			            url: 'https://github.com/gk230597/multibranch.git']]])
                }
            }
            stage("Delete the workspace after build done"){
                steps{
                    cleanWs()
                }
            }
            stage("Build"){
                steps{
                    script{
                        sh "echo build from QA"
                    }     
                }
            }
            stage("Removing the config files"){
                steps{
                    script{
                    sh "echo remove config files -QA" 
                    }
                }
            }
            stage("Stoping IIS service"){
                steps{
                    sh "echo stoping IIS - QA"
                }
            }
            stage("Taking Backup of files"){
                steps{
                    sh "echo taking backup -QA"
                }
            }
            stage("copying files"){
                steps{
                    sh "echo copying build files - QA"
                }
            }
            stage("Starting IIS Server"){
                steps{
                    sh "echo starting IIS -QA"
                }
            }
            stage('PostBuild-Email') {
                steps {
                    emailext attachLog: true, 
                    body: '$DEFAULT_CONTENT', 
                    postsendScript: '$DEFAULT_POSTSEND_SCRIPT', 
                    presendScript: '$DEFAULT_PRESEND_SCRIPT', 
                    replyTo: '$DEFAULT_REPLYTO', 
                    subject: '$DEFAULT_SUBJECT', 
                    to: 'gkgithub22@gmail.com'
                }
            }                      
        }
        stage("Staging"){
            when {
                branch 'Staging'
            }
            stage("SCM"){
                steps{
                    checkout([$class: 'GitSCM', 
			            branches: [[name: '*/Staging']], 
			            extensions: [], 
			            userRemoteConfigs: [[ 
			            url: 'https://github.com/gk230597/multibranch.git']]])
                }
            }
            stage("Delete the workspace after build done"){
                steps{
                    cleanWs()
                }
            }
            stage("Build"){
                steps{
                    script{
                        sh "echo build from Staging"
                    }     
                }
            }
            stage("Removing the config files"){
                steps{
                    script{
                    sh "echo remove config files -Staging" 
                    }
                }
            }
            stage("Stoping IIS service"){
                steps{
                    sh "echo stoping IIS - Staging"
                }
            }
            stage("Taking Backup of files"){
                steps{
                    sh "echo taking backup -Staging"
                }
            }
            stage("copying files"){
                steps{
                    sh "echo copying build files - Staging"
                }
            }
            stage("Starting IIS Server"){
                steps{
                    sh "echo starting IIS -Staging"
                }
            }
            stage('PostBuild-Email') {
                steps {
                    emailext attachLog: true, 
                    body: '$DEFAULT_CONTENT', 
                    postsendScript: '$DEFAULT_POSTSEND_SCRIPT', 
                    presendScript: '$DEFAULT_PRESEND_SCRIPT', 
                    replyTo: '$DEFAULT_REPLYTO', 
                    subject: '$DEFAULT_SUBJECT', 
                    to: 'gkgithub22@gmail.com'
                }
            } 
        }
        stage("master"){
            when {
                branch 'main'
            }
            stage("Delete the workspace after build done"){
                steps{
                    cleanWs()
                }
            }
            stage("SCM"){
                steps{
                    checkout([$class: 'GitSCM', 
			            branches: [[name: '*/main']], 
			            extensions: [], 
			            userRemoteConfigs: [[ 
			            url: 'https://github.com/gk230597/multibranch.git']]])
                }
            }
            stage("Delete the workspace after build done"){
                steps{
                    cleanWs()
                }
            }
            stage("Build"){
                steps{
                    script{
                        sh "echo build from main"
                    }     
                }
            }
            stage("Removing the config files"){
                steps{
                    script{
                    sh "echo remove config files -main" 
                    }
                }
            }
            stage("Stoping IIS service"){
                steps{
                    sh "echo stoping IIS - main"
                }
            }
            stage("Taking Backup of files"){
                steps{
                    sh "echo taking backup -main"
                }
            }
            stage("copying files"){
                steps{
                    sh "echo copying build files - main"
                }
            }
            stage("Starting IIS Server"){
                steps{
                    sh "echo starting IIS -main"
                }
            }
            stage('PostBuild-Email') {
                steps {
                    emailext attachLog: true, 
                    body: '$DEFAULT_CONTENT', 
                    postsendScript: '$DEFAULT_POSTSEND_SCRIPT', 
                    presendScript: '$DEFAULT_PRESEND_SCRIPT', 
                    replyTo: '$DEFAULT_REPLYTO', 
                    subject: '$DEFAULT_SUBJECT', 
                    to: 'gkgithub22@gmail.com'
                }
            }
        }
    }
    post{
        always{
            when{
                branch 'QA'
            }
            script{
            def jobName = currentBuild.fullDisplayName
            def result = currentBuild.result
            emailext body: '[Jenkins] ${jobName}', 
            recipientProviders: [[$class: 'DevelopersRecipientProvider']],
            to: 'gkgithub22@gmail.com', 
            subject: '[Jenkins] ${jobName} ${result}'
            }
        }
        failure{
            when{
                branch 'Staging'
            }
            script{
                def jobName = currentBuild.fullDisplayName
                emailext attachLog: true,
                body: '', 
                recipientProviders: [[$class: 'DevelopersRecipientProvider']], 
                subject: '[Jenkins] ${jobName} FAIL'
            }
        }
        unstable{
            when{
                branch 'Staging'
            }
            script{
                def jobName = currentBuild.fullDisplayName
                emailext attachLog: true,
                body: '',
                to: 'gkgithub22@gmail.com',
                subject: '[Jenkins] ${jobName} UNSTABLE'
            }
        }
        always{
            when{
                branch 'main'
            }
            script{
            def jobName = currentBuild.fullDisplayName
            def result = currentBuild.result
            emailext emailext attachLog: true,
            body: '${jobName} ${result}', 
            recipientProviders: [[$class: 'DevelopersRecipientProvider']],
            subject: '[Jenkins] ${jobName} ${result}'
            }
        }        
    }
}
