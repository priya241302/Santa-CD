pipeline {
    agent any 
    
    
    stages{
        
        stage("Git Checkout"){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/priya241302/Santa-CD.git'
        }
        }
         stage('Update GIT') {
             steps{
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                      
                        sh "git config user.email haripriyapogaku@gmail.com"
                        sh "git config user.name priya241302"
                      
                        sh "cat deploymentservice.yaml"
                        sh "sed -i 's+priya247/secreatsanta.*+priya247/secreatsanta:${DOCKERTAG}+g' deploymentservice.yaml"
                        sh "cat deploymentservice.yaml"
                        sh "git add ."
                        sh "git commit -m 'By Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Santa-CD.git HEAD:main" 


                        
                    }    
        }
    }
  }
        }
    }
}
