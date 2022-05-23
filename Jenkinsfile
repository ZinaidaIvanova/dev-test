@NonCPS
def remoteImageTag
def projectName  = 'Test dev'
def repositoryName  = 'dev-test'
def imageTag        = env.BRANCH_NAME
def ecRegistry      = "https://registry.citronium.com/v2/${repositoryName}"

node {
    try {
      stage("Checkout") {
        echo "Current ${env.BRANCH_NAME} chosen ${BRANCH_NAME} "
        // git branch: "${BRANCH_NAME}", url: 'git@github.com:ZinaidaIvanova/dev-test.git'
        def now = new Date()
        remoteImageTag = "${now.format("yyMMdd", TimeZone.getTimeZone('UTC'))}_${imageTag}_${BUILD_NUMBER}"
      }

      stage("Start") {
        echo "Build start ${remoteImageTag}\n\n${env.JOB_URL}"
      }

      stage("Docker build") {
        sh "ls"
        sh "docker build -t ${repositoryName}:${remoteImageTag} ."
      }

      stage('Up') {
          sh "docker-compose -p demoserver up -d"
      }

      stage("Notify") {
        echo "Build is completed ${remoteImageTag}\n\n${env.JOB_URL}"
      }

    } catch(e) {
      echo "Build is failed ${remoteImageTag}\n\n${env.JOB_URL}"
      throw e
    }
}