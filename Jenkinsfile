pipeline {
    agent any
    parameters {
        string(name: 'NAME',defaultValue:'mahesh babu', description:'who to greet')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    }
    environment {
                ENVIRONMENTPIPE = "pipeline level"
    }
    stages{
        stage("STAGE1"){
            environment {
                ENVIRONMENTSTAGE1 = "stage1 level"
    }
            steps{
                echo "enviormentvar: ${ENVIRONMENTPIPE}"
                echo "enviormentvar: ${ENVIRONMENTSTAGE1}"
                echo "this is stage 1"
                sh '''
                echo "NAME: ${NAME}"
                echo "CHECK:$TOGGLE"
                echo "CHOOSE:$CHOICE"
                sleep 5
                '''

            }
        }
         stage("STAGE2"){
            steps{
                echo "enviormentvar: ${ENVIRONMENTPIPE}"
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