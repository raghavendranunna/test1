node {
def mvnHome = tool 'Maven3'

stage ('Checkout') {

checkout scm
}

stage ('Build') {
sh "${mvnHome}/bin/mvn clean install -f MyWebApp/pom.xml"
} 


stage ('Code quality scan') {
withSonarQubeEnv('SonarQube') { 
sh "${mvnHome}/bin/mvn sonar:sonar -f MyWebApp/pom.xml"
   }
}


    


stage ('DEV Deploy') {
echo "deploying to DEV tomcat "
sh 'sudo cp /var/lib/jenkins/workspace/$JOB_NAME/MyWebApp/target/MyWebApp.war /var/lib/tomcat8/webapps'
}

stage ('DEV Approve') {
echo "Taking approval from DEV"
timeout(time: 7, unit: 'DAYS') {
input message: 'Do you want to deploy?', submitter: 'admin'
     }

 }



stage ('Slack notification') {


    slackSend(channel:'channel-name', message: "Job is successful, here is the info -  Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")


  }

}
