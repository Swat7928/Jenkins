pipeline {
    agent none

    triggers {
        githubPush()  // Trigger on push to GitHub
    }

    stages {
        stage('Clone to Test Node') {
            agent { label 'test' }  // Run on test node
            steps {
                script {
                    echo "Cloning repo on test node..."
                    sh "rm -rf ~/test-deploy"
                    sh "git clone --branch develop https://github.com/Swat7928/Jenkins.git ~/test-deploy"
                }
            }
        }

        stage('Clone to Prod Node') {
            agent { label 'prod' }  // Run on prod node
            when {
                expression { currentBuild.currentResult == 'SUCCESS' }
            }
            steps {
                script {
                    echo "Cloning repo on prod node..."
                    sh "rm -rf ~/prod-deploy"
                    sh "git clone --branch develop https://github.com/Swat7928/Jenkins.git ~/prod-deploy"
                }
            }
        }
    }
}
