pipeline {
    agent any
    parameters{
        string(name: 'NAME',defaultValue:'mahesh babu', description:'who to greet')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    }
    stages{
        stage("STAGE1"){
            steps{
                echo "this is stage 1"
                sh '''
                echo "NAME: $NAME"
                echo "CHECK:$TOGGLE"
                echo "CHOOSE:$CHOICE"
                sleep 5'''

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