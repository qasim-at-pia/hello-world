pipeline {
  agent {
    kubernetes {
        yaml """\
        metadata:
          labels:
            app: jenkins-agent
        spec:
          serviceAccountName: jenkins-admin
          volumes:
            - name: docker-socket
              emptyDir: {}
          containers:
            - name: jnlp
              image: jenkins/inbound-agent:latest
            - name: docker
              image: docker:27.1.2-alpine3.20
              command:
                - sleep
              args:
                - 99d
              volumeMounts:
                - name: docker-socket
                  mountPath: /var/run
            - name: docker-daemon
              image: docker:27.1.2-dind-alpine3.20
              securityContext:
                privileged: true
              volumeMounts:
                - name: docker-socket
                  mountPath: /var/run
      """.stripIndent()
    }
  }
  stages {
    stage('Sleep') {
      steps {
        sh "chmod +x ./hello.sh"
        sh "./hello.sh"
      }
    }
  }
}
