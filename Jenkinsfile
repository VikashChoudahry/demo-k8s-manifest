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
					sh "git config user.email servikash@gmail.com"
					sh "git config user.name Vikash Choudhary"
					//sh "git switch master"
					sh "cat ./overlays/local/flaskdemo/image-version.patch.yaml"
					sh "sed -i 's+msvkc1902/test-app.*+msvkc1902/test-app:${DOCKERTAG}+g' ./overlays/local/flaskdemo/image-version.patch.yaml"
					sh "cat ./overlays/local/flaskdemo/image-version.patch.yaml"
					sh "git add ."
					sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
					sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/k8s-manifest.git HEAD:development"
      			}
    		}
  		}
	}
}
