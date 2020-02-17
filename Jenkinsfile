pipeline {
    agent { docker { image 'argoproj/argo-cd-ci-builder:v0.13.1' } }
    stages {
        stage('build') {
            steps {
              sh "git clone https://github.com/ramazancetinn/argo-test-deploy.git"
              sh "ls"
              sh "git config --global user.email 'ci@ci.com'"
              dir("argocd-demo-deploy"){
                sh "cd ./prod && kustomize edit set image ramazancetinn/hellonode:latest"
                sh "git commit -am 'Publish new version' && git push || echo 'no changes'"
              }
            }
        }
    }
}
