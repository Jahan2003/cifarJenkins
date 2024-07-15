pipeline{
  agent any
  stages{
    stage('Setup'){
      steps{
        withPythonEnv('/usr/bin/python3.12'){
        sh ''
        }
      }
    }
    stage('Installation'){
      steps{
        withPythonEnv('/usr/bin/python3.12'){
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
        def logPath = "/var/lib/jenkins/jobs/pipelineJob/builds/${BUILD_NUMBER}/log"
        withPythonEnv('/usr/bin/python3.12'){
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
