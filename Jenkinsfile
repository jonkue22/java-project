properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git 'https://github.com/jonkue22/java-project.git'
		sh 'ant -f test.xml -v'   
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Results') {    
		junit 'reports/result.xml'   
	}
	stage('Report') {    
		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'   
	}
}
