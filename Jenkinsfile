pipeline{
    agent any 

    stages{
        stage("manage EC2 Instance"){
            steps{
                script{
                    def instanceId = params.INSTANCE_ID
                    def action = params.ACTION
                    switch (action) {
                        case 'start':
                          sh "aws ec2 start-instances --instance-ids ${instanceId}"
                          echo "Instance ${instanceId} starting"
                          break
                        case 'stop':
                          sh "aws ec2 stop-instances --instance-ids ${instanceId}" 
                          echo "Instance ${instanceId} stopping"
                          break 
                        case 'reboot':
                          sh "aws ec2 reboot-instances --instance-ids ${instanceId}"
                          echo "Instance ${instanceId} rebooting"
                          break
                        case 'terminate':
                          sh "aws ec2 terminate-instances --instance-ids ${instanceId}"
                          echo "Instance ${instanceId} terminating"
                          break    
                        default:
                          echo "Invalid action: ${action}"
                          break
                    }
                }
            }
        }
        stage('varify status'){
            steps {
                script {
                    echo "waiting 30 seconds for state change"
                    sleep 30
                    def status = sh(script: "aws ec2 describe-instances --instance-ids ${params.INSTANCE_ID} --query 'Reservations[0].Instances[0].State.Name' --output text", returnStdout :true).trim()
                    echo "status is ${status}"
                }
            }
        }
    }
}