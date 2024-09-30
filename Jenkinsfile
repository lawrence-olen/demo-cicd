def secret = 'global'
def vmapps = 'crocox@10.148.0.4'
def dir    = '/home/crocox/backend'
def branch = 'main'

pipeline {
    agent any
    stages {
        stage ("pull") {
            steps {
                sshagents([secret]){
                    sh """ssh -o StrictHostKeyChecking=no ${vmapps} << EOF
                    cd ${dir}
                    git pull origin ${branch}
                    echo "Git pull telah selesai"
                    exit
                    EOF"""
                }
            }
        }
        stage ("build"){
            steps {
                sshagent([secret)]{
                    sh """ssh -o StrictHostKeyChecking=no ${vmapps} << EOF
                    cd ${dir}
                    npm install
                    echo "Installasi dependensi telah selesai"
                    exit
                    EOF"""
                }
            }
        }
        stage ("run"){
            steps {
                sshagent([secret)]{
                    sh """ssh -o StrictHostKeyChecking=no ${vmapps} << EOF
                    cd ${dir}
                    pm2 start ecosystem.config.js
                    echo "Aplikasi sudah berjalan"
                    exit
                    EOF"""
                }
            }
        }    
    }
}
