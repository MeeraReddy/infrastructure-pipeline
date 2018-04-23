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
    
      sh "aws ec2 run-instances --image-id ami-467ca739 --count 1 --instance-type t2.micro --key-name MeeraKeyPair --security-group-ids sg-5e916829 --subnet-id subnet-83a4ccde --region us-east-1"
        
    }
    
    stage ("superTask") {

      def output = sh returnStdout: true, script: 'aws ec2 describe-instances | jq .'
    }
}
