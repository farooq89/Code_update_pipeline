pipeline{
   agent any
   stages{
      stage('login server'){
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
}