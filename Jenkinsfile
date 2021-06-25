node {
  def buildMap = [:]
  stage ('Checkout SCM') {
    checkout scm
  }
  stage ('Detect changed directories') {
    def lastSuccessfulBuildCommit = getLastSuccessfulCommit()
    def changedDirs = sh(
       script: """git diff ${lastSuccessfulBuildCommit} --name-only | cut -f1 -d"/" | sort -u""",
       returnStdout: true)
   echo changedDirs
   changedDirs.split("\n").each{dir -> if (!dir.equals("Jenkinsfile")) {buildMap[dir] =  {load "${dir}/Jenkinsfile"}}}
  }
  stage('Build') {
    parallel(buildMap)
  }
}

def getLastSuccessfulCommit() {
   def lastSuccessfulBuild = currentBuild.rawBuild.getPreviousSuccessfulBuild()
   def lastBuild = lastSuccessfulBuild.actions.find { action -> action instanceof hudson.plugins.git.util.BuildData }.lastBuild
   return lastBuild?.revision?.getSha1String()
}
