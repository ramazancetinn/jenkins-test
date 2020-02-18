pipeline {
    agent any
    stages {
        stage('build') {
            environment {
                GIT_CREDS = credentials('git')
            }
            steps {
                sh "echo $GIT_CREDS_USR"
                sh "rm -rf argo-test-deploy || true"
                sh "git config --global user.name 'kentkart@ci.com'"
                sh "git config --global user.email 'kentkart@ci.com'"
                sh "git clone https://github.com/ramazancetinn/argo-test-deploy.git"
              dir("argo-test-deploy"){
                sh "ls -la"
                sh "cd ./prod && kustomize edit set image ramazancetinn/hellonode:8"
                withCredentials([usernamePassword(credentialsId: 'git', passwordVariable: $GIT_CREDS_PSW, usernameVariable: $GIT_CREDS_USR)]) {
                    sh("git commit -am 'Publish new version' && git push https://github.com/ramazancetinn/argo-test-deploy.git")
                }
              }
            }
        }
    }
}
