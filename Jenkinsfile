node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email abhijeetnikam1995@gmail.com"
                        sh "git config user.name abhijeetnikam1995"
                        //sh "git switch master"
                        sh "cat result-deployment.yaml"
                        sh "sed -i 's+abhijeetnikam1995/result.*+abhijeetnikam1995/results:${DOCKERTAG}+g' result-deployment.yaml"
                        sh "cat result-deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/result-manifest.git HEAD:main"
      }
    }
  }
}
}
