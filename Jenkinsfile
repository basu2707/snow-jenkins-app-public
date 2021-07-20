pipeline {
  agent any

  environment {
    APPSYSID = '19bf1a441be9b490a104a688b04bcb5d'
    APPSCOPE = 'snow-jenkins-app-public'
    BRANCH = "${BRANCH_NAME}"
    CREDENTIALS = 'snow-jenkins-app-public'
    DEVENV_URL = 'https://comcastteamdev3.service-now.com/'
    TESTENV_URL = 'https://comcasttest.service-now.com/'
    //PRODENV_URL = 'https://prodinstance.service-now.com/'
    TESTSUITEID = 'b1ae55eedb541410874fccd8139619fb'
  } 
  stages {
    stage('Build') {
      when {
        not {
          branch 'master'
        }
      }
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV_URL}", credentialsId: "${CREDENTIALS}")
        snPublishApp(credentialsId: "${CREDENTIALS}", appSysId: "${APPSYSID}", url: "${DEVENV_URL}", appVersion: "1.0")
      }
    }
    stage('Deploy to Test') {
      when {
        branch 'master'
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${TESTENV_URL}", appSysId: "${APPSYSID}", appScope: "${APPSCOPE}", appVersion: "1.0.0")
      }
    }
  }
}
