node {
  def buildMap = [:]
  stage ('Checkout SCM') {
    checkout scm
  }
  stage ('Detect changed directories') {
    def changedDirs = sh(
       script: "git diff --name-only | sort -u",
       returnStdout: true)
   echo changedDirs
  }
  stage('Build') {
    parallel(
	proj1:{
		  load 'proj1/Jenkinsfile'
	},
    api2: {load 'api2/Jenkinsfile'})
  }
}
