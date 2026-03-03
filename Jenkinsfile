pipeline {
    agent any

    stages {
        stage('STAGE1') {
            steps {
                script{
                try{
               echo "This is stage1 running"
               sh '''
                   sleep 5
                   exit 1
               '''
               }
               catch(err){
                echo "ERROR caught: ${err}"
                currentBuilt.result = 'SUCCESS'
               }
                }
            }
        }
        
        stage('PARALLEL TESTING') {
            parallel {
                stage('WINDOWS TESTING') {
                    steps {
                    echo "This is WINDOWS testing running"
                    sh 'sleep 5'
                    }
                }

                stage('MACOS TESTING') {
                    steps {
                        echo "This is MACOS testing running"
                        sh 'sleep 5'
                    }
                }
            }
        }

        stage('FINAL') {
            steps {
               echo "This is FINAL running"
               sh 'sleep 5'
            }
        }
    }
}