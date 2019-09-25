pipeline {
    agent any

    

    stages {
        
        
        

        stage ('Deploy to EC2') {
          steps {
              withCredentials([string(credentialsId: 'ansible-vault-pwd', variable: 'ansible_vault_pwd')]) {
    ansiblePlaybook(
                playbook: 'playbook1.yml',
                colorized: true,
                vaultCredentialsId: 'ansible-vault-pwd'
    )
              }            
            
          }
        }

    }
}
