pipeline {
    agent any
    options { 
        disableConcurrentBuilds(abortPrevious: true)
        timeout(time: 1, unit: 'HOURS')
        }

    stages {
        stage('CHECKOUT') {
            steps{
                checkout ([ $class: 'GitSCM',
                    branches: [[name: '*/main']], 
                    extensions: [], 
                    userRemoteConfigs: [[
                        credentialsId: 'github',
                        url: 'https://github.com/ajith007-web/MyGitpractice.git'
                        ]]
                ])
            }
        }
        stage('stage') {
            when {
                expression {
                    return env.GIT_BRANCH == 'origin/main'
                }
            }
             steps{
                sh'''
                   pwd
                   git branch
                   ls -lrt
                '''
             }
        }
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
            steps {
               echo "This is FINAL running"
               sh 'sleep 5'
            }
        }
    }
}
