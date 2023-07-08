node{
    stage('git checkout')
    {
        git branch: 'master', url: 'https://github.com/chandanadevopslearn/chandana-Banking-finance-project.git'
    }

    stage('maven compile'){
    
    sh 'mvn clean compile'
    }
    stage('maven-test'){
        
    sh 'mvn clean test'
    }
    stage('maven-package'){
        
    sh 'mvn clean package'
    }
    stage('dockerimagebuild')
    {
    sh 'sudo docker build -t mchandana123/chandanabanking:1.0 .'
   
    }
    stage('docker image push to registry')
    {
    
    withCredentials([string(credentialsId: 'dockercred', variable: 'dockercred')]) {
        sh 'docker login -u mchandana123 -p ${dockercred}'
        sh 'docker push mchandana123/chandanabanking:1.0'
    
}
    }
    stage('deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'ansible', disableHostKeyChecking: true, installation: 'myansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}

