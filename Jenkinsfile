pipeline{
  agent any
  stages{
    stage('Setup'){
      steps{
        WithPythonEnv('/usr/bin/python3.12'){
        sh 'sudo apt-get install -y python3-venv python3-pip'
        }
      }
    }
    stage('Installation'){
      steps{
        WithPythonEnv('/usr/bin/python3.12'){
        sh 'pip3 install -r requirements.txt'
         }
      }
    }
    stage('Run'){
      steps{
        WithPythonEnv('/usr/bin/python3.12'){
        sh 'python3 inference.py'
        }
      }
    }
    stage('Storage'){
      steps{
        script{
        def logPath = "/var/lib/jenkins/jobs/pipelineJob/builds/${BUILD_NUMBER}/log"
        WithPythonEnv('/usr/bin/python3.12'){
        sh "cp ${logPath} ${WORKSPACE}/log"
        archiveArtifacts artifacts: 'log', allowEmptyArchive: true
        }
        }
      }
    }
  }
  post{
    always{
      withPythonEnv('/usr/bin/python3.12'){
      sh "aws s3 cp ${WORKSPACE}/log s3://jenkinsserverbucket/build/${BUILD_NUMBER}/"
      }
    }
  }
}
