node('new43') {
// Delete the workspace
//deleteDir()
     def app
stage('Retrieve source code') {
    checkout scm
    delivery = load 'repository.groovy'
 sh " cd $WORKSPACE;/bin/mkdir Build-${env.BUILD_NUMBER} "
    }
try {
 stage('build artifact') {
         sh "mvn clean package -Dbuild.number=${BUILD_NUMBER}"
       }
       stage('Publish') {
     nexusPublisher nexusInstanceId: 'localNexus', nexusRepositoryId: 'releases', packages: [[$class: 'MavenPackage', mavenAssetList: [[classifier: '', extension: '', filePath: 'war/target/jenkins.war']], mavenCoordinate: [artifactId: 'jenkins-war', groupId: 'org.jenkins-ci.main', packaging: 'war', version: '2.23']]]
   }
       
        }
  catch (e) {
      currentBuild.result = "FAILED"
      throw e
    }
}
