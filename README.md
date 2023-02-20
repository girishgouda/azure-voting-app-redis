
az k8s-configuration flux create -g gitopscluster \
-c gitopscluster \
-n demoapp \
--namespace  demoapp \
-t managedClusters \
--scope cluster \
-u https://github.com/girishgouda/azure-voting-app-redis.git \
--branch master  \
--kustomization name=infra path=./infradeploy prune=true \
--kustomization name=app path=./appdeploy prune=true dependsOn=\["infra"\]  \
--kustomization name=post path=./postdeploy prune=true dependsOn=\["app"\]