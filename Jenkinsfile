pipeline {
    agent {
      label 'node1'
    }
    environment {
        appUser = "shoeshop"
        appName = "shoe-ShopingCart"
        appVersion = "0.0.1-SNAPSHOT"
        appType = "jar"
        processName = "${appName}-${appVersion}.${appType}"
        buildScript = "mvn clean install -Dskiptest"

    }
    stages {
        stage('info') {
            steps {
                sh(script: """ whoami;pwd;ls -la """, label: "firt stage")
            }
        }
        stage('build'){
            steps{
                sh(script: """ ${buildScript} """, label: "build with maven")
            }
        }
    }
}
