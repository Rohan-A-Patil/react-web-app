
pipeline {
 agent any 
 tools {
    nodejs 'node'  
  }
 stages {
   stage('Build') {
     steps {
       script {
         cleanWs()
         checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '${GITBranch}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/vmgponly/react-web-app.git']]] 
        }
      }
   
    }  
    
  }  
  
}  
