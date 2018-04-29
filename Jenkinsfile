properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Test') {    
		git 'https://github.com/jonkue22/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'  
	}
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}
	stage('Deploy') {    
		sh 'aws s3 cp rectangle-12.jar s3://jenkins/data/'
	}
	stage('Report') {
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    			sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'  
		}
	}
}
