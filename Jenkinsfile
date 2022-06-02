pipeline {
    agent any
     stages {
	stage('Clone Repo') {
    	  steps {
	    sh 'rm -rf dockertest1'
      	    sh 'git clone https://github.com/chandu42142/dockertest1.git'
	 }
  }

	stage('Build Docker Image') {
           steps {
	    sh 'cd /var/lib/jenkins/workspace/pipelinetest1/dockertest1'
	    sh 'cp /var/lib/jenkins/workspace/pipelinetest1/dockertest1/* /var/lib/jenkins/workspace/pipelinetest1'
	    sh 'docker build -t gnapi9642/pipelinetest:v2 .'
	 }
 }
	stage('Push Image to Docker Hub') {
           steps {
	    sh	'docker push gnapi9642/pipelinetest:v2'
	 }
 }
	stage('Deploy to Docker Host') {
           steps {
	    
	    sh 'docker -H tcp://10.1.1.200:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 gnapi9642/pipelinetest:v1'
	 }
}
	stage('Check WebApp Rechability') {
          steps {
	   sh 'sleep 10s'
	   sh 'curl http://ec2-54-160-149-85.compute-1.amazonaws.com:9000'
	 }
}
}
}
