pipeline{
   agent any
   stages{
      stage('Code Update'){
         steps{
            sshagent(credentials:['134']){
               // sh 'ssh  -o StrictHostKeyChecking=no  frappe@192.168.10.134 "pwd"'
               script {
                        sh '''
                            ssh -o StrictHostKeyChecking=no frappe@192.168.10.134 "
                                cd frappe-bench/apps/associated_terminals \\
                                && git stash \\
                                && git pull \\
                                && cd dashboard \\
                                && npm install \\
                                && yarn build
                            "
                        '''
               }
        echo "Build complete"
            }
         }
      }
   }
   post {
        always {
            script {
                slackSend(channel: '#atd-notifications', color: 'good', message: "134 code updated!")
            }
        }
        failure {
            script {
                // test123123
                slackSend(channel: '#atd-notifications', color: 'danger', message: "Build failed!")
            }
        }
    } 
}