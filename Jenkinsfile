pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "rm -rf argo-test-deploy || true"
                sh "ls -la"
                sh "pwd"
                sh "git config --global user.email 'kentkart@ci.com'"
                sh "git clone https://github.com/ramazancetinn/argo-test-deploy.git"
              dir("argo-test-deploy"){
                sh "ls -la"
                sh "cd ./prod && kustomize edit set image ramazancetinn/hellonode:latest"
                sh "git commit -am 'Publish new version' && git push origin master || echo 'no changes'"
              }
            }
        }
    }
}
