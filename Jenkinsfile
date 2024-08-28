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
                echo "Build carried out using MSBuild."
            }
        }
        stage('Test'){
            steps{
                echo "Unit tests carried out using MSTest."
                echo "Integration tests carried out using MSTest."
            }
            post{
                always{
                    sendEmail("Test")
                }
            }
        }
        stage('Code Analysis'){
            steps{
                echo "Code analysis carried out using PMD."
            }
        }
        stage('Security Scan'){
            steps{
                echo "Security scan carried out using HCL AppScan."
            }
            post{
                always{
                    sendEmail("Security Scan")
                }
            }
        }
        stage('Deploy to Staging'){
            steps{
                echo "Deployed to staging area on AWS Cloud Server."
            }
        }
        stage('Integration Tests'){
            steps{
                echo "Integration tests carried out using MSTest."
            }
        }
        stage('Deploy to Production'){
            steps{
                echo "Deployed to production area on AWS Cloud Server."
            }
        }
    }
}

def sendEmail(stage){
    emailext (
        to: "$EMAIL",
        subject: "${stage} Status Email",
        body: "Stage - ${stage} - has finished.\nStatus is ${currentBuild.currentResult}.\nLogs are attached.",
        attachLog: true)
}
