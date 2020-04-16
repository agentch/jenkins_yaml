# Jenkins integrates kubernetes
kubectl apply -f opspvc.yml -f rbac.yml -f secret.yaml -f jenkins-deployment.yml