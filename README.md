####the application named "drkiq" ######
it depends on "postgres and redis"
the env variable as "CACHE URL" passed to container through configmap.
the secret data as database password and username passed through secrets.
################################################
please follow the below steps to deploy the app on k8s.

1-kubect create -f env-configmap.yaml -n [namespace]
2-kubect create -f rails-secrets.yaml -n [namespace]
3-kubect create -f postgres.yaml -n [namespace]
4-kubect create -f redis.yaml -n [namespace]
5-please wait till redis and postgres pods are up and running.
6-kubect create -f reset-database-job.yml -n [namespace]  ----> to create database and run the migration if exists
7-kubect create -f railsapp.yaml -n [namespace]
8-kubect create -f sidekiq.yaml -n [namespace]
9-kubect create -f nginx.yaml -n [namespace]  ---> to create nginx as reverse proxy and make it access externally via port 30600


#we can package the app by helm/ kudo to automate the installation and  manage the dependencies.
