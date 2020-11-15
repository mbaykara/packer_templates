node() {
  //def app
  checkout scm

  def String dockerImage = 'celcin/runtime-tool'
  def String dockerArgs = "-v ${WORKSPACE}/conan:/tmp/conan" 

  
  stage('Testing') {
    parallel (
      'Release Build': {
        docker.image(dockerImage).inside(dockerArgs) {
            echo " Hello rest"
         
            sh   "curl -fsSL https://apt.releases.hashicorp.com/gpg |  apt-key add - "
            sh   "apt-add-repository  deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
            sh   "apt-get update &&  apt-get install packer"
            sh "packer version"
/* 
           sh '''#!/bin/bash
                echo " Hello rest"
                 curl -fsSL https://apt.releases.hashicorp.com/gpg |  apt-key add -
                 apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main
                 apt-get update &&  apt-get install packer
         '''  */
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