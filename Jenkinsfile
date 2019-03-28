node {
stage ('Build') {

    stage('Initialize') {
        // Get some code from a GitHub repository
        def dockerHome = tool '321'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
    stage('Clone Repository') {
        // Get some code from a GitHub repository
        git 'https://bitbucket.org/RenatsA/spring-petclinic-renats2.git'
    
   }
   stage('Deploy on tomcat'){
   sshagent(['tomcat-dev']) {
    sh "scp -o StrictHostKeyChecking=no target/* .war ec2-user@52.213.91.16:/opt/tomcat8/webapps/"
}
}
   
   stage('Deploy Spring Boot Application') {
        
         //Remove maven-build-container if it exists
        sh " docker rm -f java-deploy-container"
       
        sh "docker run --name java-deploy-container --volumes-from maven-build-container -d -p 8089:8089 denisdbell/petclinic-deploy"
   }
}
}