node('ubuntu18.04-OnDemand'){

stage('scm checkout'){
  cleanWs()
  
  checkout scm
}

stage('build SupplyChainTools package'){
  sh 'mvn clean package'
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