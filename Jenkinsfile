pipeline{
  agent any
  stages{
    stage('Run'){
      steps{
        sh 'pwd'
        sh 'python3 inference.py'
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
