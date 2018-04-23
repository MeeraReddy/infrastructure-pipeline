properties([pipelineTriggers([githubPush()])])
node('linux') {
    git url: 'https://github.com/MeeraReddy/infrastructure-pipeline.git', branch: 'master'
    stage('Test') {
        sh "env"
    }
    
    
    // Get the EC@ instances
    stage ("GetInstances") {

       sh "aws ec2 describe-instances --region us-east-1"
    }
    

    // Create EC2 instances
    stage ("CreateInstance") {
    
        
    }
    
    
}
