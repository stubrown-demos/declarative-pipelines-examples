# dec_kaniko_build_publish

A Kubernetes secrets is required for this example

kubectl create secret docker-registry docker-credentials \
    --docker-username=<username>  \
    --docker-password=<password> \
    --docker-email=<email-address>
