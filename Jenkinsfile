pipeline {
    agent {
      label 'node1'
    }
    stages {
        stage('info') {
            steps {
                sh(script: """ whoami;pwd;ls -la """, label: "firt stage")
            }
        }
    }
}
