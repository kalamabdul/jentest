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
    stage('vault') {
      environment {
        VAULT_ADDR="https://vault.kalamabdul.com:8200"
        AIT_NUM="12345"
      }
      steps {
        withCredentials([string(credentialsId: 'org-token', variable: 'IDTOKEN')]) {
          container('vault') {
            sh 'vault write -field=token auth/jwt/login role=bu3-teama-frontend-application jwt=${IDTOKEN} > token'
            sh 'echo ${JENKINS_HOME}'
            sh 'echo ${AIT_NUM}'
            sh '''
              echo $IDTOKEN | base64 > tmp
               '''
            sh 'cat tmp'
            sh 'cat token'
            sh 'set +x ; VAULT_TOKEN=$(cat token) vault read -field=data -format=json secrets/data/org/bu1/teama'
          }
        }
      }
    }
  }
}
