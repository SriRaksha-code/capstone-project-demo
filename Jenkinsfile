node{

    stage('code checkout'){
        git 'https://github.com/SriRaksha-code/capstone-project-demo.git'
    }
    
    stage('build'){
      sh 'mvn clean package'  
    }
    
    stage('containerize'){
      sh 'docker build -t raksha07/insure-me:1.0 .'
    }
    
    stage('push to dockerhub'){
      withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerhubpwd')]) {
            sh "docker login -u raksha07 -p ${dockerhubpwd}"
            sh 'docker push raksha07/insure-me:1.0'
        }
    }
    
    stage('deploy') {
        ansiblePlaybook become: true, credentialsId: 'ansible-ssh-jenkins-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'config-test-server.yml'
    }

}
