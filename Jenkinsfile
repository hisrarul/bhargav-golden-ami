pipeline {
    agent { node { label 'master' } }

    stages {
      stage('Preparation') {
             steps {
                 echo 'Fetching files from git..'
                 sh "git clone https://github.com/hisrarul/bhargav-golden-ami.git"
             } 
         }
        stage('Logged-In user') {
            steps {
            sh """ echo 'Logged-In User'
                    id """ }
        }
    stage('Baking AMI') {
      steps {
        echo 'Baking AMI..'
        script{
          sh """ if ./packer --version; then
                 echo "packer already installed"
                 else
                     wget https://releases.hashicorp.com/packer/1.4.2/packer_1.4.2_linux_amd64.zip
                     unzip packer_1.4.2_linux_amd64.zip
                     rm -rf packer_1.4.2_linux_amd64.zip
                 fi
                ./packer validate bhargav-golden-ami/template.json
                ./packer build bhargav-golden-ami/template.json """ }
            }
        }
    stage('Wipe out workspace') {
                steps {
                    deleteDir()
                }
        }
    }
  }
