pipeline {
    agent any
    
    environment {
        slackChannel = '#se-jenkins'
        // latestStage = 'Start'
        jenkinsIcon = 'https://wiki.jenkins-ci.org/download/attachments/2916393/logo.png'
    }

    stages {
//         stage('git clone'){
//             steps {
//                 git branch: 'dev', url: 'https://github.com/stackexpress-jawed/demo01.git'
//             }
            
//         }
        
        stage('docker run') {
            steps {
                sh 'sleep 10'
                sh 'docker run hello-world'
            }
        }
        
        // stage('custom error') {
        //     steps {
        //         error "Program failed..."
        //     }
        // }
    }
    
    post {
        success {
            slackSend color: 'good',
            channel: "${slackChannel}",
            message: """
                Pipeline: <${env.BUILD_URL}/console|${env.JOB_NAME}>
                Git branch: `${env.GIT_BRANCH}`
                Build number: *${env.BUILD_DISPLAY_NAME}*
                Build status: *${currentBuild.result}*
                Total runtime: *${currentBuild.durationString}*
            """.stripIndent()
        }

        failure {
            slackSend color: 'danger',
            channel: "${slackChannel}",
            message: """
                Pipeline: <${env.BUILD_URL}/console|${env.JOB_NAME}>
                Git branch: `${env.GIT_BRANCH}`
                Build number: *${env.BUILD_DISPLAY_NAME}*
                Build status: *${currentBuild.result}*
            """.stripIndent()
        }
        
    }
    
}
