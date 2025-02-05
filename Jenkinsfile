pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/kr-aman3107/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t kraman3107/2febimg:v1'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'kraman3107')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push kraman3107/2febimg:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 kraman3107/2febimg:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 akshu20791/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.2.113 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.46.37 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
