pipeline{
  agent any
  stages{
    stage('Setup'){
      steps{
        echo pwd
        // sh 'sudo apt-get update'
        // sh 'sudo apt-get install -y python3-venv python3-pip'
      }
    }
    stage('Virtual Environment Creation'){
      steps{
        echo pwd
        // sh 'python3 -m venv pyenv'
      }
    }
    stage('Installation'){
      steps{
        echo pwd
        // sh '. pyenv/bin/activate && pip3 install -r requirements.txt'
      }
    }
    stage('Run'){
      steps{
        echo pwd
        // sh '. pyenv/bin/activate && python3 inference.py'
      }
    }
    stage('Storage'){
      steps{
        // archiveArtifacts artifacts: 'log', allowEmptyArchive: true
      }
    }
  }
}
