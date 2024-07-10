pipeline{
  agent any
  stages{
    stage('Setup'){
      steps{
        echo "Setup"
        // sh 'sudo apt-get update'
        // sh 'sudo apt-get install -y python3-venv python3-pip'
      }
    }
    stage('Virtual Environment Creation'){
      steps{
        sh 'python3 -m venv pyenv'
      }
    }
    stage('Installation'){
      steps{
        sh '. pyenv/bin/activate && pip3 install -r requirements.txt'
      }
    }
    stage('Run'){
      steps{
        sh '. pyenv/bin/activate && python3 inference.py'
      }
    }
  }
  post{
    always{
      sh 'rm -rf pyenv'
    }
  }
}
