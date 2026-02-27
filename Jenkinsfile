pipeline {
    stages {
        stage("STAGE1"){
            steps{
                echo "this is stage 1"
                sh 'sleep 5'
            }
        }
         stage("STAGE2"){
            steps{
                echo "this is stage 2"
                sh '''
                #!/bin/bash
                pwd
                ls -lrt
                sleep 5
                '''
            }
        }
    }
}