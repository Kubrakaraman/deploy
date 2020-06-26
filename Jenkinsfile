pipeline {
    agent any
     parameters {
    gitParameter name: 'version', 
            type: 'PT_TAG',
            defaultValue: 'master'
    }
         stages{
             stage('Checkout') {
             steps{
                checkout([$class: 'GitSCM', 
                          branches: [[name: "${version}"]], 
                          doGenerateSubmoduleConfigurations: false, 
                          extensions: [], 
                          gitTool: 'Default', 
                          submoduleCfg: [], 
                          userRemoteConfigs: [[url: 'https://gitlab.com/EVKURAN/jenkinscase.git']]
                        ])
                 }    
            }
            stage('Docker build') {
              steps {
                  
               sh " docker build -t kubramydocker/${name}:${version} . "
                }
             }
             stage('Docker Push') {
              steps {

               sh " docker push kubramydocker/${name}:${version}  "
                }
             }
             
              stage('Docker Deploy') {
              steps {
 
               sh " docker run -tid --name nginx kubramydocker/${name}:${version} "

                }
             }
          }
    }
