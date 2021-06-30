pipeline {
    agent any
    
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
                     withCredentials([string(credentialsId: "55c80c17-91f3-487d-b7ad-3b13b13443b2", variable: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI1NWM4MGMxNy05MWYzLTQ4N2QtYjdhZC0zYjEzYjEzNDQzYjIiLCJpYXQiOjE2MjUwMzUzNTIsImlzcyI6ImFyZ29jZCIsIm5iZiI6MTYyNTAzNTM1Miwic3ViIjoicHJvajpkZWZhdWx0OmplbmtpbnMifQ.uezAcODaOUMhj67U10Fw2fsnsjyyNnfSBdtx1enBfP4')]) {
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
