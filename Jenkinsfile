def getEnvForBD(branch) {
  if(env.BRANCH_NAME == 'master'){
    return 'test2'
    }else {
      return 'test1'
    }
  } 
pipeline{
    agent none

    environment{
      ENVIRONMENT = getEnvForBD(env.BRANCH_NAME)
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
                                    catch(error){
                                        env.VERSION = 1.0
                                        env.SCRIPT = 'Baseline'
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
