pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "rm -rf argo-test-deploy || true"
                sh "git config --global user.name 'kentkart@ci.com'"
                sh "git config --global user.email 'kentkart@ci.com'"
                sh "git clone https://github.com/ramazancetinn/argo-test-deploy.git"
              dir("argo-test-deploy"){
                sh "ls -la"
                sh "cd ./prod && kustomize edit set image ramazancetinn/hellonode:latest"
                withCredentials([usernamePassword(credentialsId: 'git', passwordVariable: 'DEXter1905', usernameVariable: 'ramazancetinn')]) {
                    sh("git commit -am 'Publish new version' && git push https://${ramazancetinn}:${DEXter1905}@github.com/ramazancetinn/argo-test-deploy.git")
                }
              }
            }
        }
    }
}
