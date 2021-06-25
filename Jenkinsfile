pipeline{
    agent none
    stages{
        stage('test1') {
            agent {
                label 'master'
            }
            stages {
                stage('Inicio') {
                    steps {
                      withCredentials([usernamePassword(credentialsId: 'SAP-Credentials', passwordVariable: 'PASSWORD_PDN', usernameVariable: 'USER_PDN'),
                                       usernamePassword(credentialsId: 'CuentasQA-BD', passwordVariable: 'PASSWORD_QA', usernameVariable: 'USER_QA')]){
                        script {
                            env.PASSWORD = 'PASSWORD_QA'
                            env.USER = 'USER_QA'
                            if(env.BRANCH_NAME == 'master'){
                                env.PASSWORD = 'PASSWORD_PDN'
                                env.USER = 'USER_PDN'
                              }
                            echo "Obteniendo Plan for ${USER}"

                            }
                      }
                        }
                    }
                }
            }
        }
    }
  
