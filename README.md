# test-syncfail
test sync fail
<!-- 


       stage ('Deploy_K8S') {
             steps {
                     withCredentials([string(credentialsId: "jenkins", variable: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiIyMmJkOTQ2MC0zNTk3LTQ4NjMtYjk5ZC0zMzI4NzkzMTcyNzAiLCJpYXQiOjE2MjQ5ODYyMjQsImlzcyI6ImFyZ29jZCIsIm5iZiI6MTYyNDk4NjIyNCwic3ViIjoicHJvajpkZWZhdWx0OmplbmtpbiJ9.g5CS88AkDfopn9sET55g6LS6l7BGy9giKR4t1636fVI')]) {
                        sh "ARGOCD_SERVER=localhost:8080 argocd --grpc-web app sync haha --force"
                        
                        
                        '''
                        // We won't use below command template since we are using minikube for the demo.
                        // ARGOCD_SERVER="argocd-prod.example.com"
                        // APP_NAME="debian-test-k8s"
                        // CONTAINER="k8s-debian-test"
                        // REGION="eu-west-1"
                        // AWS_ACCOUNT="$ACCOUNT_NUMBER"
                        // AWS_ENVIRONMENT="staging"

                        // $(aws ecr get-login --region $REGION --profile $AWS_ENVIRONMENT --no-include-email)
                        
                        # Deploy image to ECR
                        docker tag $CONTAINER:latest $AWS_ACCOUNT.dkr.ecr.$REGION.amazonaws.com\$CONTAINER:latest
                        docker push $AWS_ACCOUNT.dkr.ecr.$REGION.amazonaws.com\$CONTAINER:latest
                        IMAGE_DIGEST=$(docker image inspect $AWS_ACCOUNT.dkr.ecr.$REGION.amazonaws.com\$CONTAINER:latest -f '{{join .RepoDigests ","}}')
                        # Customize image 
                        ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app set $APP_NAME --kustomize-image $IMAGE_DIGEST
                        
                        # Deploy to ArgoCD
                        ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app sync $APP_NAME --force
                        ARGOCD_SERVER=$ARGOCD_SERVER argocd --grpc-web app wait $APP_NAME --timeout 600
                        '''
               }
            }
        } -->
