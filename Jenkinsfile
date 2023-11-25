node{    
    stage('code checkout'){
        git branch: 'main', credentialsId: 'abhi144k@gmail.com', url: 'https://github.com/AKS144/star-agile-health-care.git'
    }    
    stage('code build'){
        sh 'mvn clean install'
    }    
    stage('containerize'){
        sh 'docker build -t abhi144k/health:1.0 .'
    }       
    stage('push on docker'){     
        withCredentials([string(credentialsId: 'dockerhubpsd', variable: 'dockerhubpsd')]) {
            sh "docker login -u abhi144k -p ${dockerhubpsd}"
            sh 'docker push abhi144k/health:1.0'
        }
    }  
    stage('deploy'){
    ansiblePlaybook become: true, disableHostKeyChecking: true, installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml', vaultTmpPath: ''
    	
    }  
}
