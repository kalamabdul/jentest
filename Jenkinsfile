pipeline {
    agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: vault
            image: hashicorp/vault
            command:
            - cat
            tty: true
      '''
    }
  }
  stages {
    stage('hello') {
      steps {
        sh 'echo "Hello World"'
      }
    }
  }
}
