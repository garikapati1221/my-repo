@Library("app-lib") _
pipeline{
    agent any
     tools {
  maven 'maven3'
}
options {
  buildDiscarder logRotator(daysToKeepStr: '10', numToKeepStr: '7')
}
parameters {
  choice choices: ['develop', 'qa', 'master'], description: 'choice the branch to build', name: 'branchName'
}
stages{
        stage('Git Clone'){
            steps{
            git branch: branchName, credentialsId: 'git_repo', url: 'https://github.com/garikapati1221/my-repo'
            }
            
        }
         stage('Maven Build'){
            steps{
               // sh '/var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven3/bin/mvn clean package'
               sh 'mvn clean package'
            }
            }
            
         stage('Deploy to tomcat'){
            steps{
              
              // sshagent(['tomcat-dep']) {
                   tomcatDeploy(["54.254.178.35","54.254.178.35","54.254.178.35"],"ec2-user","tomcat-dep")
    // some block
     // sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.31.101:/opt/tomcat8/webapps/app.war"
     // sh "ssh ec2-user@172.31.31.101 /opt/tomcat8/bin/startup.sh"
    //  sh "ssh ec2-user@172.31.31.101 /opt/tomcat8/bin/shutdown.sh"

            }
            }
           
            
    }
    post {
  success {
    // One or more steps need to be included within each condition's block.
    archiveArtifacts artifacts: 'target/*.war'
    cleanWs()
  }
}

}
