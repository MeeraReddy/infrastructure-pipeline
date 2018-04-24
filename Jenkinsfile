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
    
      //sh "aws ec2 run-instances --image-id ami-467ca739 --count 1 --instance-type t2.micro --key-name MeeraKeyPair --security-group-ids sg-5e916829 --subnet-id subnet-83a4ccde --region us-east-1"
     sh "aws ec2 run-instances --image-id ami-467ca739 --count 1 --instance-type t2.micro --key-name MeeraKeyPair --security-group-ids sg-e7dea7ae --subnet-id subnet-177b9e4b --region us-east-1"
        
    }
    
    stage ("superTaskTerminate") {
        
       def op = sh returnStdout: true, script: 'aws ec2 describe-instances --filters Name=vpc-id,Values=vpc-ac973bc9 --query 'Reservations[].Instances[].[PrivateIpAddress,InstanceId,Tags[?Key==`Name`].Value[]]' --output text | sed 's/None$/None\n/' | sed '$!N;s/\n/ /''
        // get instance iD
        def output = sh returnStdout: true, script: 'aws ec2 describe-instances --region us-east-1 | jq .'
        echo output
       //waiter
       // sh "aws ec2 wait --region us-east-1 instance-running --instance-ids output"
        
      // Terminate
      //  sh "aws ec2 terminate-instances --instance-ids output"
      
    }
}
