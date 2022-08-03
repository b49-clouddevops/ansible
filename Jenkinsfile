pipeline {
    agent any 
    parameters {
         choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Chose the environment')
         string(name: 'COMPONENT', defaultValue: 'mongodb', description: 'Enter the name of the component')
    }
    environment { 
        SSH_CRED = credentials('SSH-Cenos7')
    }
    stages {
        
        stage('Lint Checks') {  // This will be executed against the feature branch only
            when { branch pattern: "feature-.*", comparator: "REGEXP"}
            steps {
                sh "env"
                sh "echo Style Checks"
                sh "echo running is feature branch"
            }
        } 

        stage('Do a dry-run') {        // This will be executed only when you raise a PR, PR's will only be detected if you use the GitHub Plugin
        when { branch pattern: "PR-.*", comparator: "REGEXP"}
            steps {
                sh "env"   // Just to see tne environment variables as a part of the pipeline
                sh "ansible-playbook robot-dryrun.yml -e ansible_user=${SSH_CRED_USR} -e ansible_password=${SSH_CRED_PSW} -e COMPONENT=${params.COMPONENT} -e ENV=${params.ENV}"
            }
        }

        stage('Promote to Prod') {
            when { branch 'main' }       
            steps {
                sh "echo Runs only when you push a git tag"
            }
        }
    }
}