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
                    sh 'docker build -t mazood/akshatnewimg6july:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub_pwd', passwordVariable: 'mazood', usernameVariable: 'mazood')]) {
                    sh 'docker login -u ${dockerhub_pwd} -p ${mazood}'
                    sh 'docker push mazood/akshatnewimg6july:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 mazood/akshatnewimg6july:v1'
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
