pipeline {
	agent any
	stage(‘Build’) {
		sh ‘ant’
	}
	stage(‘Test’) {
		junit ‘reports/result.xml’
	}
}
