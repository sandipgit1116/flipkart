pipeline {
	agent{
	label 'slave1'
	}
	parameters {
		choice(name: 'ENVIRONMENT', choices: ['QA','UAT'], description: 'Pick Environment value')
	}
	stages {
	    stage('Checkout') {
	        steps {
			checkout scm			       
		      }}
		stage('Build') {
	           steps {
			  sh '/home/user1/slaveDD1/apache-maven-3.9.1/mvn install'
	                 }}
		stage('Deployment'){
		    steps {
			sh 'sshpass -p "dev" scp target/flipkart.war user1@172.17.0.2:/home/user1/slaveDD1/apache-tomcat-9.0.73/webapps'
			}}
		stage('Docker build'){
		    steps {
			sh 'docker build -t sandipdocker1116/pipelineimage11.1.2 .'
			}}
		stage('Docker Login'){
		    steps {
		withCredentials([string(credentialsId: 'sandipdocker1116', variable: 'docker-sandipdocker')]) {
    		sh 'docker login -u sandipdocker1116 -p${docker-Sandip@1116}'                 
			echo 'Login Completed'
			}
			
			}}
		stage('Push Image to Docker Hub') {         
    		    steps{                            
 			sh 'docker push sandipdocker1116/pipelineimage11.1.2:$BUILD_NUMBER'           
			echo 'Push Image Completed'       
    			}}
		
}}
