pipeline {
    agent {
      label 'node1'
    }
    environment {
        appUser = "shoeshop"
        appName = "shoe-ShopingCart"
        appVersion = "0.0.1-SNAPSHOT"
        appType = "jar"
        folderDeploy = "/datas/${appUser}"
        processName = "${appName}-${appVersion}.${appType}"
        buildScript = "mvn clean install -Dskiptest"
        copyScript = "sudo cp target/${processName} ${folderDeploy}"
        perScript = "sudo chown -R ${appUser}:${appUser} ${folderDeploy}"
        killScript = "sudo kill \$(ps -ef | grep ${processName} | grep -v grep | awk '{print \$2}')"
        runScript = 'sudo su ${appUser} -c "cd ${folderDeploy}; java -jar ${processName} > nohup.out 2>&1 &"'

    }
    stages {
        stage('info') {
            steps {
                sh(script: """ whoami;pwd;ls -la;sudo mkdir -p ${folderDeploy} """, label: "firt stage")
            }
        }
        stage('build'){
            steps{
                sh(script: """ ${buildScript} """, label: "build with maven")
            }
        }
        stage('Deploy'){
            steps{
                sh(script: """ ${copyScript} """, label: "copy the .jar into deploy folder")
                sh(script: """ ${perScript} """, label: "set permission folder")
                //sh(script: """ ${killScript} """, label: "terminate the running process")
                sh(script: """ ${runScript} """, label: "run the project")

            }
        }
    }
}
