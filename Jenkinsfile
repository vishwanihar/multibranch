properties([[$class: 'GithubProjectProperty', displayName: '', projectUrlStr: 'https://github.com/vishwanihar/multibranch.git/'], pipelineTriggers([upstream('docker, dockerinstall, dockerbuild'), githubPush()])])
node {
 	// Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
        	checkout scm
        }
        stage ('Build') {
        	sh "echo 'shell  to build project...'"
        }
        stage ('Tests') {
	        parallel 'static': {
	            sh "echo 'shell scripts to rstatic tests...'"
	        },
	        'unit': {
	            sh "echo 'shell scripts to run unit tests...'"
	        },
	        'integration': {
	            sh "echo 'shell scripts to run integration tests...'"
	        }
        }
      	stage ('Deploy') {
            sh "echo 'shells to deploy to server...'"
		
      	}
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}



