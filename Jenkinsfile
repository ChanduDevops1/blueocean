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
	    sh 'cd /var/lib/jenkins/workspace/blueocean_main/dockertest1'
	    sh 'cp /var/lib/jenkins/workspace/blueocean_main/dockertest1/* /var/lib/jenkins/workspace/blueocean_main'
	    sh 'docker build -t gnapi9642/blueoceanmain:v1 .'
	 }
 }
	stage('Push Image to Docker Hub') {
           steps {
	    sh	'docker push gnapi9642/blueoceanmain:v1'
	 }
 }
	stage('Deploy to Docker Host') {
           steps {
	    sh 'docker -H tcp://10.1.1.200:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 gnapi9642/blueoceanmain:v1'
	 }
}
	stage('Check WebApp Rechability') {
          steps {
	   sh 'sleep 10s'
	   sh 'curl http://ec2-3-90-207-126.compute-1.amazonaws.com:9000'
	 }
}
}
}
