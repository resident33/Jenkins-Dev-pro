pipeline {
    agent any
    parameters {
        string(name: 'Ip', defaultValue: 'name', description: 'Ip or dnsname instance')
        string(name: 'User', defaultValue: 'user', description: 'Enter username for ssh')
        string(name: 'sshkey', defaultValue: 'empty', description: 'Enter key for ssh')
        }
       stages {
        stage ('Connect to instance'){
            steps {
                     sh 'mkdir ~/.ssh'
                     sh 'touch ~/.ssh/key.pem'
                     sh "echo ${params.sshkey} | sed -e 's/ /\\n/g' > ~/.ssh/key.pem"
                     sh "sed -i '1,4d' ~/.ssh/key.pem | sed -i -n -e :a -e '1,4!{P;N;D;};N;ba' ~/.ssh/key.pem"
                     sh "sed -i '1i -----BEGIN RSA PRIVATE KEY-----' ~/.ssh/key.pem"
                     sh "echo '-----END RSA PRIVATE KEY-----' >> ~/.ssh/key.pem"
                     sh 'cat ~/.ssh/key.pem'
                     sh 'chmod 700 ~/.ssh'
                     sh 'chmod 600 ~/.ssh/key.pem'
                     print 'Good'
                     sh "ssh -o 'StrictHostKeyChecking no' -i ~/.ssh/key.pem ${params.User}@${params.Ip}"
                     sh "exit"
                     print "Connect to Instance: Done"
              }
        }

        stage ('Install enviroment'){
            steps{
                sh "ssh -t -i ~/.ssh/key.pem ${params.User}@${params.Ip} 'sudo apt update -y'"
                sh "ssh -t -i ~/.ssh/key.pem ${params.User}@${params.Ip} 'sudo apt install nodejs npm git -y'"
                print "Install enviroment: Done"
            }
        }

        stage ('Git Clone'){
            steps{
                sh "ssh -t -i ~/.ssh/key.pem ${params.User}@${params.Ip} 'mkdir ~/nodejs-api'"
                sh "ssh -t -i ~/.ssh/key.pem ${params.User}@${params.Ip} 'git clone https://github.com/geerlingguy/demo-nodejs-api.git ~/nodejs-api'"
                print "Git Clone: Done"
            }
        }

        stage ('Build'){
            steps{
                sh "ssh -t -i ~/.ssh/key.pem ${params.User}@${params.Ip} 'cd /home/${params.User}/nodejs-api && npm install'"
                sh "id"
                print "Build: Done"
            }
        }

        stage ('Test'){
            steps{
                sh "ssh -t -i ~/.ssh/key.pem ${params.User}@${params.Ip} 'cd /home/${params.User}/nodejs-api && npm test'"
                print 'Test: Done'
            }
        }

        stage ('Cleaning'){
            steps{  
                sh "ssh -t -i ~/.ssh/key.pem ${params.User}@${params.Ip} 'sudo rm -R /home/${params.User}/nodejs-api'"
                sh 'exit'
                sh 'rm -R ~/.ssh'
                print 'Cleaning: Done'

            }
        }
    }

    post {
        always {
                emailext body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
              }
         }
}
