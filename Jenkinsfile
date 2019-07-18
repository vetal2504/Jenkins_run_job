pipeline {
    agent any

    stages {
        stage('Create instance') {
            steps {
                sh "ansible-playbook create_instance.yml --vault-password-file=/home/ubuntu/ansible/pass.txt --extra-vars ansible_sudo_pass=jenkins"
            }
        }
        stage('Get all instances instances') {
            steps {
                sh "aws ec2 describe-instances --filters \"Name=instance.group-name,Values=newInstance\" --query \"Reservations[*].Instances[*].PublicIpAddress\" --output=text \
                    > hosts"
            }
	}
	stage('Test available instances') {
            steps {
		sh "sudo ansible all -i hosts -m ping --private-key=/home/ubuntu/ansible.pem -u ubuntu"
		}
        }
        stage ('Manage instances') {
		steps {
		sh "ansible-playbook manage.yml -i hosts -f 5 --private-key=/home/ubuntu/ansible.pem -u ubuntu"
		}
	}
    }
}
