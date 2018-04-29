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
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    			sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'  
		}
	}
}
