pipeline {
    agent any

    environment {
        ANSIBLE_HOSTS = '<your_inventory>'
        PLAYBOOK = '<your_playbook.yaml>'
        BACKUP_DIR = '/tmp/ssh_backup'
        GIT_REPO = '<your_playbook_repo>'
        GIT_BRANCH = '<your_branch>' // or the specific branch where the playbook is located
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        stage('Clone Repository') {
            steps {
                script {
                    // Clone the Git repository containing the playbook
                    sh "git clone -b ${GIT_BRANCH} ${GIT_REPO} playbook-repo"
                }
            }
        }

        stage('Setup') {
            steps {
                script {
                    // Ensure the SSH configuration directory exists on all hosts
                    ansibleCommand("ansible all -i ${ANSIBLE_HOSTS} -m file -a \"path=/etc/ssh state=directory\"")
                }
            }
        }



        stage('Update sshd_config') {
            steps {
                script {
                    // Set LoginGraceTime to 0
                    ansibleCommand("ansible-playbook -i ${ANSIBLE_HOSTS} playbook-repo/${PLAYBOOK}")
                }
            }
        }

    }

    post {
        always {
            // Archive the backup directory to Jenkins artifacts
            archiveArtifacts artifacts: "${BACKUP_DIR}/**", allowEmptyArchive: true
        }
    }
}

def ansibleCommand(command) {
    sh "${command}"
}
