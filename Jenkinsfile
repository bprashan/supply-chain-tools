node(){
// requires java-11-openjdk-amd64 for compilation

try{
// try-catch block is used to test email notifications

stage('scm checkout'){
  // this stage checkout the code from the Git repo
  
  cleanWs() // wipe out the build workspace before checkout
  
  checkout scm 
}

stage('build SupplyChainTools package'){
  // builds the sct package
  sh '''
  export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
  export PATH=$JAVA_HOME/bin:$PATH
  mvn clean package  
  '''
}

stage('archeive artifacts'){
  sh '''
    mkdir -p SupplyChainTools
    cp -r manufacturer-webapp/target/manufacturer-webapp-*.war $WORKSPACE/SupplyChainTools
    cp -r reseller-webapp/target/reseller-webapp-*.war $WORKSPACE/SupplyChainTools
  '''

    zip zipFile: 'SupplyChainTools.zip', archive: false, dir: 'SupplyChainTools'
    archiveArtifacts artifacts: 'SupplyChainTools.zip', fingerprint: true, allowEmptyArchive: false
    // sends the mail to the developers if the build is successful.
    emailext body: '', recipientProviders: [developers()], subject: ''
}

}
catch (err){
// sends the mail to the culprits and developers if build failure
    currentBuild.result = "FAILURE"
    emailext body: '', recipientProviders: [developers(), culprits()], subject: ''
    throw err
}

}