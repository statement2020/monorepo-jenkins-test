node {
  stage ('Checkout SCM') {
    checkout scm
  }
  parallel(
	proj1:{
		  load 'proj1/Jenkinsfile'
	},
  api2: {load 'api2/Jenkinsfile'}
}
