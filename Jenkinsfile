  
pipeline {

environment { registry = "" 
              registryCredential = '' 
              dockerImage = '' 
           }
agent any 

stages {

stage ('clone') {
     git(
       url: 'git clone https://github.com/vijji432/kubernetes-for-java-developers.git',
       credentialsId: 'git',
       branch: "master"
    )
}  
  stage ('build docker image') {
  steps { 
    script { dockerImage = docker.build registry + ":$BUILD_NUMBER" 
     }
  }
 stage('Deploy our image to dockerhub') { 
           steps {
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }
        } 
stage ('deploy') {
steps {
    ansiblePlaybook credentialsId: 'ansib-jenk', installation: 'ansibl', inventory: '/etc/ansible/hosts', playbook: '/var/lib/jenkins/workspace/kubernetes-for-java-developers/app'
  }
 }
}
}
}
