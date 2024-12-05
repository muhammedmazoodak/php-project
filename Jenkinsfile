pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/muhammedmazoodak/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t mazood/bankingproject-demo:1.0 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-login', passwordVariable: 'dockerlogin', usernameVariable: 'dockerlogin')]) {
                    sh 'docker login -u ${docker-login} -p ${dockerlogin}'
                    sh 'docker push mazood/bankingproject-demo:1.0'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 mazood/bankingproject-demo:1.0'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 akshu20791/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.29.195 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.29.195 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
