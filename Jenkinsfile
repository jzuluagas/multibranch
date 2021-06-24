pipeline{
    agent none

    triggers{
        bitbucketPush()
    }

    options { 
        buildDiscarder(logRotator(numToKeepStr: '10')) 
        disableConcurrentBuilds() 
    }
    script {
        env.ENVIRONMENT = 'test2'
        if(env.BRANCH_NAME == 'master'){
            env.ENVIRONMENT = 'test1'
        }
    }
    stages{
        stage('test1') {
            stages {
                stage('Inicio') {
                    steps {
                        script {
                            echo "La IP es: "
                            sh "curl 'https://api.ipify.org?format=text'"
                            env.IP = sh(script: "curl 'https://api.ipify.org?format=text'", returnStdout: true).trim()

                            withCredentials([usernamePassword(credentialsId: ${ENVIRONMENT}, passwordVariable: 'PASSWORD', usernameVariable: 'USER')]){
                                dir('./'){
                                    try{
                                        sh "cat $USER"
                                        sh "echo $PASSWORD >> pass"
                                        sh "cat pass"
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}