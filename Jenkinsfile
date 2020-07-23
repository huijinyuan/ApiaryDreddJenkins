// use node 12
node('node12') {
   stage('Get source code') {
      git url: 'https://github.com/huijinyuan/ApiaryDreddJenkins', branch: 'master'
   }
   stage('Install Deps') {
      if(isUnix()) {
         sh 'node -12'
         sh 'npm -6'
         sh 'npm install'
         sh 'npm -g install dredd@13.1.2'
      } else {
         bat 'node -12'
         bat 'npm -6'
         bat 'npm install'
         bat 'npm -g install dredd@13.1.2'
      }
   }  
   stage('Test API Blueprint') {
      if(isUnix()) {
         wrap([$class: 'AnsiColorBuildWrapper', 'colorMapName': 'XTerm']) {
          sh 'dredd --config ./apiblueprint/dredd.yml --reporter junit --output blueprint.xml'
         }
      } else {
         bat 'dredd --config ./apiblueprint/dredd.yml --reporter junit --output blueprint.xml'
      }
   }
   stage('Get JUnit Results') {
      junit 'blueprint.xml'
   }
}
