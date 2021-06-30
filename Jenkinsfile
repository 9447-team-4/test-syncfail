pipeline {
    agent {
        node {
            label 'testing'
        }
    }
    
    stages {       
        stage('Prepare') {
            steps {
                checkout([$class: 'GitSCM',
                branches: [[name: "origin/main"]],
                doGenerateSubmoduleConfigurations: false,
                submoduleCfg: [],
                userRemoteConfigs: [[
                    // source code repo
                    url: 'https://github.com/9447-team-4/test-syncfail.git']]
                ])
            }
        }
        stage ('Deploy_K8S') {
             steps {
                     withCredentials([string(credentialsId: "argo", variable: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI0MjQxNTU0NS01NDc4LTQ5NWYtYjk1Ni1jNTEzNmU3ZjZjYTYiLCJpYXQiOjE2MjUwMzQ0MzgsImlzcyI6ImFyZ29jZCIsIm5iZiI6MTYyNTAzNDQzOCwic3ViIjoicHJvajpkZWZhdWx0OmplbmtpbnMifQ.uOKvp1WJKEKpZsoIlqGmvlM2SxYdecOdvbQ65Mec-3k')]) {
                        sh 'export pwd=$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo)'
                  
                        sh "echo $pwd"
                        sh "argocd login localhost:8080 --username admin --password $pwd --grpc-web"
                        
                        sh "ARGOCD_SERVER=localhost:8080 argocd --grpc-web app sync a --force"
                        sh "ARGOCD_SERVER=localhost:8080 argocd --grpc-web app sync a --timeout 600"
                    
               }
            }
        }
        stage ('Run_fuzzer') {
            steps {
                echo "Hi fuzzer"
            }
        }
    }
    post {
        // always {
        //     echo "HIHIHIHI"
        // }
        success {
            echo "SUCCESS"
        }
        failure {
            echo "FAIL"
        }
    }
    
}
