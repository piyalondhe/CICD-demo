
pipeline 
{
  agent any

  
  stages {
      
       stage ('clone')
    {
        steps{
        git 'https://github.com/piyalondhe/CICD-demo.git'
             }
    }

       stage ('build')
    {
        steps{
            sh label: '', script: 'mvn clean package'
             }
    }
    
       stage ('deploy')
    {
        steps{
        sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /root/.ansible/roles/
ansible-galaxy install zaxos.tomcat-ansible-role
rm -rf CICD-demo
git clone https://github.com/piyalondhe/CICD-demo.git
ansible-playbook CICD-demo/tomcat_install.yml
ansible-playbook CICD-demo/app_deploy.yml''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//root/', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'target/mvn-hello-world.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
             }
    }
     
   
          }
     
}
