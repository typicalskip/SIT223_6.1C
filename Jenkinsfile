pipeline { 
    agent any
    environment{
        DIRECTORY_PATH = "My/Directory/Path"
        TESTING_ENVIRONMENT = "SIT223"
        PRODUCTION_ENVIRONMENT = "Tim Mackey"
    }

    stages{
        stage('Build'){
            steps{
                echo "Fetching source code from: $DIRECTORY_PATH"
                echo "Compile code and generate any necessary artifacts."
            }
            post{
                always{
                    sendEmail("Build")
                }
            }
        }
        stage('Test'){
            steps{
                echo "Unit tests..."
                echo "Integration tests..."
            }
        }
        stage('Code Analysis'){
            steps{
                echo "Checking the quality of the code ..."
            }
        }
        stage('Security Scan'){
            steps{
                echo "Security scan complete."
            }
            post{
                always{
                    sendEmail("Security Scan")
                }
            }
        }
        stage('Deploy to Staging'){
            steps{
                echo "Deploying the application to staging."
            }
        }
        stage('Integration Tests'){
            steps{
                sleep(10)
                echo "Approved"
            }
        }
        stage('Deploy to Production'){
            steps{
                echo "Deploying to Production Environment: $PRODUCTION_ENVIRONMENT"
            }
        }
    }
}

def sendEmail(stage){
    emailext (
        to: "typicalskip88@gmail.com",
        subject: "${stage} Status Email",
        body: "Stage - ${stage} - has finished.\nStatus is ${currentBuild.currentResult}.\nLogs are attached.",
        attachLog: true)
}