pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh "ansible-playbook create_instance.yml --vault-password-file=/home/ubuntu/ansible/pass.txt --extra-vars ansible_sudo_pass=jenkins"
            }
        }
    }
}
