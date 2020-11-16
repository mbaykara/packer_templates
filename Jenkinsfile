node() {
  //def app
  checkout scm

  def String dockerImage = 'celcin/packer'
  def String dockerArgs = "-v ${WORKSPACE}/conan:/tmp/conan" 
  def String url = "https://releases.hashicorp.com/packer/0.9.0/packer_0.9.0_linux_amd64.zip"

  
  stage('Testing') {
    parallel (
      'Release Build': {
        docker.image(dockerImage).inside(dockerArgs) {
            echo " Hello rest"
            sh "packer version"
            sh "cd ${WORKSPACE}/Ubuntu-18.04 && packer build new.json"
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