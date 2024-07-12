pipeline{
  agent any
  stages{
    stage('Setup'){
      steps{
        sh 'pwd'
        sh 'sudo apt-get update'
        sh 'sudo apt-get install -y python3-venv python3-pip'
      }
    }
    stage('Virtual Environment Creation'){
      steps{
        sh 'pwd'
        sh 'python3 -m venv pyenv'
      }
    }
    stage('Installation'){
      steps{
        sh 'pwd'
        sh '. pyenv/bin/activate && pip3 install -r requirements.txt'
      }
    }
    stage('Run'){
      steps{
        sh 'pwd'
        sh '. pyenv/bin/activate && python3 inference.py'
      }
    }
    stage('Storage'){
      steps{
        script{
        def logPath = "/var/lib/jenkins/jobs/demoJob/branches/main/builds/${BUILD_NUMBER}/log"
        sh "cp ${logPath} ${WORKSPACE}/log"
        archiveArtifacts artifacts: 'log', allowEmptyArchive: true
        }
      }
    }
  }
  post{
    always{
      sh "aws s3 cp ${WORKSPACE}/log s3://jenkinsserverbucket/build/${BUILD_NUMBER}/"
    }
  }
}
