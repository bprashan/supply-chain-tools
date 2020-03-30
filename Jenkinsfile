node(){

stage('scm checkout'){
  cleanWs()
  
  checkout scm
}

stage('build SupplyChainTools package'){
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
}

}