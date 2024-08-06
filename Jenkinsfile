pipeline {
  agent {
    kubernetes {
        yaml """\
        metadata:
          labels:
            app: jenkins-agent
        spec:
          serviceAccountName: jenkins-admin
          containers:
            - name: jnlp
              image: jenkins/inbound-agent:latest
      """.stripIndent()
    }
  }
  stages {
    stage('Sleep') {
      steps {
        sh "sudo chmod +x ./hello.sh"
        sh "./hello.sh"
      }
    }
  }
}
