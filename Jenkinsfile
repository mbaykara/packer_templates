node() {
  //def app
  checkout scm

  def String dockerImage = 'celcin/runtime-tool'
  def String dockerArgs = "-v ${WORKSPACE}/conan:/tmp/conan" 

  
  stage('Testing') {
    parallel (
      'Release Build': {
        docker.image(dockerImage).inside(dockerArgs) {
         
          sh '''#!/bin/bash
                 mkdir p && cd p && ${devEnv} BUILDNUMBER=${env.BUILD_NUMBER} /usr/bin/conan  new hello/0.1 -t 
                 curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
                 sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
                 sudo apt-get update && sudo apt-get install packer
         '''
        }
      },
      'Complexity': {
        docker.image(dockerImage).inside(dockerArgs) {
          sh " ls /tmp/conan"
        }
      }      
    )
  }
}