// Define your secret project token here
def project_token = 'a2662b242dd06333a2ed4dc781e4d2ab'

// Reference the GitLab connection name from your Jenkins Global configuration (https://JENKINS_URL/configure, GitLab section)
pipeline {
    agent any
    stages {

        stage('Initializing Env') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'master'){
                        echo 'Initializing Environtment'
                        sh '''sh ~/.bashrc'''
                        }
                    else if (env.BRANCH_NAME == 'development'){
                        echo 'Initializing Environtment'
                        sh '''sh ~/.bashrc'''
                        sh '''chmod +x ~/workspace/rnappsdemo_development/android/gradlew '''
                    }
                    else if (env.BRANCH_NAME == 'stage'){
                        echo 'Initializing Environtment'
                        sh '''sh ~/.bashrc'''
                    }
                }
            }
        }

        stage('Building Apps') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'master'){
                        echo 'Build Master Branch'
                        // sh '''npm install --prefer-offline --no-audit && npm run build --prefer-offline --no-audit'''
                    }
                    else if (env.BRANCH_NAME == 'development'){
                        echo 'Build Development Branch'
                        sh '''npm install --prefer-offline --no-audit'''
                        sh '''cd ~/workspace/rnappsdemo_development/android && ./gradlew assembleRelease'''
                    }
                    else if (env.BRANCH_NAME == 'stage'){
                        echo 'Build Stage Branch'
                        // sh '''npm install --prefer-offline --no-audit && npm run build --prefer-offline --no-audit'''
                    }
                }
            }
        }

        stage('Testing Apps') {
            steps{
                script{
                    if (env.BRANCH_NAME == 'master'){
                        echo 'Testing Build Result'
                    }
                    else if (env.BRANCH_NAME == 'development'){
                        echo 'Testing Build Result'
                    }
                    else if (env.BRANCH_NAME == 'stage'){
                        echo 'Testing Build Result'
                    }
                }
            }
        }
        stage('Deploy Apps') {
            steps{
                script{
                    if (env.BRANCH_NAME == 'master'){
                        echo 'Copy Build Result Master Branch Code to Server'
                        // sh '''scp -r ~/workspace/democicd_development/build padepokan79@10.10.5.17:/opt/democicd/fsmfedemo'''
                    }
                    else if (env.BRANCH_NAME == 'development'){
                        echo 'Copy Build Result Development Branch Code to Server'
                        // sh '''scp -r ~/workspace/democicd_development/build padepokan79@10.10.5.17:/opt/democicd/fsmfedemo'''
                    }
                    else if (env.BRANCH_NAME == 'stage'){
                        echo 'Copy Build Result Stage Branch Code to Server'
                        // sh '''scp -r ~/workspace/democicd_development/build padepokan79@10.10.5.17:/opt/democicd/fsmfedemo'''
                    }
                }
                discordSend description: "Jenkins Pipeline Build", footer: "Footer Text", link: env.BUILD_URL, result: currentBuild.currentResult, title: JOB_NAME, webhookURL: "https://discord.com/api/webhooks/841520042330947585/FYlL6KFUgmh9O1LCFp5yUcatPqKMdr2X_qnb4ITSMoglGQm3lfaMxQfXc6yQZ1s9L4jS"
            }
        }
    }
}