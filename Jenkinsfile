// pipeline {
//     agent any

//     stages {
//         stage("build") {
//             steps {
//                 echo 'building...'
//             }
//         }
//         stage("test") {
//             echo 'testing...'
//         }
//         stage("deploy") {
//             echo 'deploying...'
//         }
        
//     }
// }

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
                     withCredentials([string(credentialsId: "argocd-deploy-role", variable: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIyMmJkOTQ2MC0zNTk3LTQ4NjMtYjk5ZC0zMzI4NzkzMTcyNzAiLCJpYXQiOjE2MjQ5ODYyMjQsImlzcyI6ImFyZ29jZCIsIm5iZiI6MTYyNDk4NjIyNCwic3ViIjoicHJvajpkZWZhdWx0OmplbmtpbiJ9.g5CS88AkDfopn9sET55g6LS6l7BGy9giKR4t1636fVI')]) {
                        // sh "export pwd=$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo)"
                  
                        // sh "echo $pwd"
                        // sh "argocd login localhost:8080 --username admin --password $pwd --grpc-web"
                        sh "argocd login localhost:8080 --username admin --password YisYXPnZPVwEJqAJ --grpc-web"
                        
                        sh "ARGOCD_SERVER=localhost:8080 argocd --grpc-web app sync haha --force"
                        sh "ARGOCD_SERVER=localhost:8080 argocd --grpc-web app sync haha --timeout 600"
                    
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
