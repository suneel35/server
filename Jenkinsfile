#!groovy
node
{
    def MAVEN_HOME = tool name:"MAVEN_HOME", type:'maven'
    def mvnCMD = "${MAVEN_HOME}/bin/mvn"
    stage ('checkout')
    {
        git credentialsId: 'GitHub', url: 'https://github.com/suneel35/Hello_World.git'
        
    }

    stage('Build')
    {
       
        sh "${mvnCMD} package"
    
    }
    stage('Docker build')
    {
        sh 'docker build . -t hello'
    }
    stage('Docker tag')
    {
        sh 'docker tag hello suneel35/hello:latest'
    }
    stage('Docker push')
    {
        withCredentials([string(credentialsId: 'Dockerhub', variable: 'DockerHubPswd')]) {
    sh 'docker login -u suneel35 -p ${DockerHubPswd}'
}
        sh "docker push suneel35/hello:latest"
    }

    stage('Docker container')
   {
      sh 'docker run -d -p 9091:8080 --name world suneel35/hello:latest'
   }  
     
}
