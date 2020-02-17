pipeline {
    agent { docker { image 'argoproj/argo-cd-ci-builder:v0.13.1' } }
    stages {
        stage('build') {
            steps {
                sh "rm -r argo-test-deploy"
                sh "git clone https://github.com/ramazancetinn/argo-test-deploy.git"
              dir("argo-test-deploy"){
                sh "ls -la"
                sh "cd ./prod && kustomize edit set image ramazancetinn/hellonode:latest"
                sh "git config --global user.email 'kentkart@ci.com'"
                sh "git commit -am 'Publish new version' && git push || echo 'no changes'"
              }
            }
        }
    }
}
