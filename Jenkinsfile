pipeline {
    agent any

    

    stages {
        

        stage ('Deploy to EC2') {
          steps {
            
              ansiblePlaybook(
                playbook: 'playbook1.yml',
                colorized: true)
            
          }
        }

    }
}
