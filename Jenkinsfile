node {
  stage('build & deploy') {
    openshiftBuild bldCfg: 'hellopythonapp',
      showBuildLogs: 'true'
  }
  stage('approval (test)') {
    input message: 'Approve for testing?',
      id: 'approval'
  }
  stage('oc tag :test') {
    openshiftTag srcStream: 'hellopythonapp',
      srcTag: 'latest',
      destStream: 'hellopythonapp',
      destTag: 'test'
  }
  stage('oc deploy :test') {
    openshiftDeploy depCfg: 'hellopythonapp',
      namespace: 'testing'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'testing'
  }
  stage('approval (production)') {
    input message: 'Approve for production?',
      id: 'approval'
  }
  stage('oc tag :prod') {
    openshiftTag srcStream: 'hellopythonapp',
      srcTag: 'latest',
      destStream: 'hellopythonapp',
      destTag: 'prod'
  }
  stage('oc deploy :prod') {
    openshiftDeploy depCfg: 'hellopythonapp',
      namespace: 'production'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'production'
  }
}