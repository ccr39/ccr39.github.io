pipeline {
  agent any
  stages {
    stage('检出') {
      steps {
        checkout([
          $class: 'GitSCM',
          branches: [[name: env.GIT_BUILD_REF]], 
          userRemoteConfigs: [[url: env.GIT_REPO_URL, credentialsId: env.CREDENTIALS_ID]]
        ])
      }
    }
    stage('部署到腾讯云存储') {
      steps {
        sh "coscmd config -a ${env.COS_SECRET_ID} -s ${env.COS_SECRET_KEY} -b ${env.COS_BUCKET_NAME} -r ${env.COS_BUCKET_REGION}"
        sh 'rm -rf .git'
        sh 'coscmd upload -r ./ /'
      }
    }
  }
}
