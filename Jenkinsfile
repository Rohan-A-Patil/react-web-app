
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
         checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '${GITBranch}']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Rohan-A-Patil/react-web-app.git']]] 
         sh '''
         ls -ltr
         npm install 
         npm run build
         ls -ltr
         cd build
         tar -cvf frontend-${BUILD_NUMBER}.tar *
         cp frontend-${BUILD_NUMBER}.tar ${WORKSPACE}/
         cd ${WORKSPACE}
         ls -ltr
         '''
       }
      }
    } 
    stage('Deploy') {
      steps {
       sh '''
        rm -rf deploy
        mkdir deploy
        cp -r frontend-${BUILD_NUMBER}.tar deploy
        cd deploy
        tar -xvf frontend-${BUILD_NUMBER}.tar 
        rm -rf frontend-${BUILD_NUMBER}.tar
        ls -ltr
        gsutil acl ch -u AllUsers:R gs://rohan-patil
        gsutil defacl set public-read gs://rohan-patil
        gsutil web set -m index.html -e index.html gs://rohan-patil
        gsutil cp -r * gs://rohan-patil/
        gsutil setmeta -h "content-type: image/svg+xml" gs://rohan-patil/static/media/*.svg
       '''
      }
     }
    
  }  
  
}  
