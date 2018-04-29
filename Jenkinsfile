properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git 'https://github.com/jonkue22/java-project.git'
		sh 'ant -buildfile test.xml'   
	}   
	stage('Build') {    
		sh 'ant'   
	}   
	stage('Results') {    
		junit 'reports/result.xml'   
	}
}

