
pipeline{

    agent any

    tools{
        maven 'Maven'
        jdk 'JDK'

    }

    environment{
        ANSIBLE_HOST ="ubuntu@18.236.177.29"
        SSH_KEY_ID ="anisble-key"
    }

    stages{
        stage("clone rep"){
        steps{

            git url:"https://github.com/kanthireddy/app.git"
        }
    }
    
    stage("Build"){
        steps{
            sh "mvn clean package"
        }
    }

    stage("Deploy"){
        steps{
            sshagent(credentials: ['ansible-key']){
                sh '''
                    cd ansible-deploy
                    ANSIBLE_HOST_KEY_CHECKING=False ansible playbook -i hosts.ini tomcat_deploy.yml

                '''
            }
        }
    }


}
}
