@NonCPS
def remoteImageTag
def projectName  = 'Test dev'
def repositoryName  = 'dev-test'
def imageTag        = env.BRANCH_NAME
def ecRegistry      = "https://registry.citronium.com/v2/${repositoryName}"

node {
    try {
      // stage("Checkout") {
      //   git branch: "${env.BRANCH_NAME}", url: 'git@github.com:ZinaidaIvanova/dev-test.git'
      //   def commit_hash = sh(returnStdout: true, script: "git rev-parse --short HEAD").trim()
      //   def now = new Date()
      //   remoteImageTag = "${now.format("yyMMdd", TimeZone.getTimeZone('UTC'))}_${imageTag}_${BUILD_NUMBER}_${commit_hash}"
      // }

      stage("Start") {
        echo "Build start ${remoteImageTag}\n\n${env.JOB_URL}"
      }

      stage('Up') {
          sh "docker-compose up -d"
      }

      stage("Notify") {
        echo "Build is completed ${remoteImageTag}\n\n${env.JOB_URL}"
      }

    } catch(e) {
      echo "Build is failed ${remoteImageTag}\n\n${env.JOB_URL}"
      throw e
    }
}