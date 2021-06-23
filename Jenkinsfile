node {
  def buildMap = [:]
  stage ('Checkout SCM') {
    checkout scm
  }
  stage ('Detect changed directories') {
    def changedDirs = sh(
       script: """git diff HEAD~1 --name-only | cut -f1 -d"/" | sort -u""",
       returnStdout: true)
   echo changedDirs
   changedDirs.split("\n").each{dir -> if (!dir.equals("Jenksinfile")) {buildMap[dir] = load "${dir}/Jenkinsfile"}}
  }
  stage('Build') {
    parallel(buildMap)
  }
}
