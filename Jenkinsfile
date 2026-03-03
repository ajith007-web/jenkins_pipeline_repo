pipeline {
    agent any
     environment {
        CURRENT_ENV = 'prod'
    }

    stages {
        stage('STAGE1_a') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    echo "This is stage1 running"
                    sh ''' 
                        sleep 5
                        exit 1
                    '''
                }
            }
        }
        
        stage('STAGE1_b') {
            steps {
                script { 
                    try {
                        sh ''' 
                            sleep 5
                            exit 1
                        '''
                    } 
                    catch (err) {
                        echo "Error caught: ${err}"
                        currentBuild.result = 'SUCCESS'
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
            when{
                environment name: 'CURRENT_ENV', value: 'prodd'
            }
            steps {
               echo "This is FINAL running"
               sh 'sleep 5'
            }
        }
    }
}