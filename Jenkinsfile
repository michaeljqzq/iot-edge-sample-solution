def genericSh(cmd) {
  if (isUnix()) {
    sh cmd
  }
  else {
    bat cmd
  }
}

node {
  stage('Checkout') {
    checkout scm
  }

  withEnv(['DEVOPS_IOTEDGE_REGISTRY_URL=zhiqing.azurecr.io']) {
    stage('test') {
      sh "printenv"
    }
    stage('Build') {
      azureIoTEdgePush dockerRegistryType: 'acr', acrName: 'zhiqing', bypassModules: '', azureCredentialsId: 'azuresp', resourceGroup: 'iotedge-jenkins-automation-test', rootPath: './'
    }
    
    stage('Deploy') {
      azureIoTEdgeDeploy azureCredentialsId: 'azuresp', deploymentId: 'jenkins-pipeline-deploy', deploymentType: 'single', deviceId: '123', iothubName: 'jenkins-test', priority: '0', resourceGroup: 'iotedge-jenkins-automation-test', rootPath: './', targetCondition: ''
    }
  }
}
