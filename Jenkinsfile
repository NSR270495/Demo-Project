pipeline{
    agent any
    tools{
        maven "Maven-3.9.2"
    }
    stages{
        stage('Get Code'){
            steps{
                git credentialsId: 'Github-Credential', url: 'https://github.com/NSR270495/Demo-Project.git',branch: "main"
            }
        }
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
        stage('Deploy'){
            steps{
                sshagent(['ssh-key']) {
                   sh """
                   scp -o StrictHostKeyChecking=no target/DemoProject.war ubuntu@65.2.172.191:/home/ubuntu/apache-tomcat-9.0.79/webapps
                   ssh ubuntu@65.2.172.191:/home/ubuntu/apache-tomcat-9.0.79/bin/shutdown.sh
                   ssh ubuntu@65.2.172.191:/home/ubuntu/apache-tomcat-9.0.79/bin/startup.sh
                   """
                }
            }
        }
    }
}
