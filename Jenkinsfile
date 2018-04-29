properties([pipelineTriggers([githubPush()])])

node('linux') {   
	stage('Unit Tests') {    
		git 'https://github.com/jonkue22/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'  
	}
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}
	stage('Deploy') {    
		sh 'aws s3 cp $WORKSPACE/target/rectangle-11.jar s3://my-bucket-name/${env.BRANCH_NAME}/ --recursive --exclude '*' --include '*.jar''
	}
	stage('Report') {
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    			sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1'  
		}
	}
}
