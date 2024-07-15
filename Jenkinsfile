pipeline{
  agent any
  environment{
    AWS_CREDENTIALS_ID = '2d385ee4-417c-4b98-9b11-ee1d56e6680f'
  }
  stages{
    stage('Setup'){
      steps{
        withPythonEnv('/usr/bin/python3.12'){
        //setup
        sh 'python --version'
        sh 'sudo apt-get update'
        sh 'sudo apt-get install -y python3-venv python3-pip'
        sh 'pip3 install -r requirements.txt'
        }
      }
    }
    stage('Run'){
      steps{
        withPythonEnv('/usr/bin/python3.12'){
        sh 'python3 inference.py'
        }
      }
    }
    stage('Storage'){
      steps{
        script{
        def log_path = "/var/lib/jenkins/jobs/${JOB_NAME}/builds/${BUILD_NUMBER}/log"
        withPythonEnv('/usr/bin/python3.12'){
        sh "cp ${log_path} ${WORKSPACE}/log"
        archiveArtifacts artifacts: 'log', allowEmptyArchive: true
        }
        }
      }
    }
  }
  post{
    always{
      withPythonEnv('/usr/bin/python3.12'){
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: "${AWS_CREDENTIALS_ID}"]]){
      sh "aws s3 cp ${WORKSPACE}/log s3://jenkinsserverbucket/build/${BUILD_NUMBER}/"
      }
      }
    }
  }
}
