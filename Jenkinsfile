pipeline {
    agent none
    environment {
        PLUGIN_NAME = "org.idempiere.mfg"
        IDEMPIERE_VERSION = "10.0.0"
        BRANCH = "master"
        JAR_NAME = "${PLUGIN_NAME};singleton:=true-${IDEMPIERE_VERSION}.${BUILD_NUMBER}.jar"
    }
    stages {
        stage('Compile') {
            agent {
                docker {
                    image 'idempiereofficial/idempiere:source-release-10.0'
                    args '-u root:root --entrypoint='                
                  }
            }
            steps {
                dir('target-platform') {
                    git branch: '10', url: 'https://github.com/ingeint/idempiere-target-platform-plugin.git'
					sh './plugin-builder build ../../${PLUGIN_NAME}_${BRANCH}'
                    archiveArtifacts artifacts: "target/${JAR_NAME}", fingerprint: true
                    
                }
            }
        }
      
    }
}
