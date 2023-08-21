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
                   sh "scp -o StrictHostKeyChecking=no target/DemoProject.war ubuntu@43.205.178.54:/home/ubuntu/apache-tomcat-9.0.79/webapps"
                //   sh "cd ubuntu@43.205.178.54:/home/ubuntu/apache-tomcat-9.0.79/bin/"
                //   sh "sh shutdown.sh
                //   sh "cd ubuntu@43.205.178.54:/home/ubuntu/apache-tomcat-9.0.79/bin/"
                //   sh "sh startup.sh"
                }
            }
        }
    }
}
