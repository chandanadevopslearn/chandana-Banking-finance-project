node{
    stage('git checkout')
    {
        git branch: 'master', url: 'https://github.com/Akhil2598/akhil-banking-finance-project.git'
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
    sh 'sudo docker build -t akhil2598/akhilbanking:1.0 .'
   
    }
    stage('docker image push to registry')
    {
    
    withCredentials([string(credentialsId: 'dockercred', variable: 'dockercred')]) {
        sh 'docker login -u akhil2598 -p ${dockercred}'
        sh 'docker push akhil2598/akhilbanking:1.0'
    
}
    }
    stage('deploy')
    {
    
       ansiblePlaybook become: true, credentialsId: 'akhil', disableHostKeyChecking: true, installation: 'myansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}

