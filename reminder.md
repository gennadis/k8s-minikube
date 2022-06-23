# Pushing images
eval $(minikube docker-env)
docker build -t django .
kubectl run django --image=django_app --image-pull-policy=Never --env SECRET_KEY=123123dsafsdf

# Executing commands
kubectl exec django -ti -- python manage.py migrate
kubectl exec django -ti -- python manage.py shell
kubectl exec django -ti -- python manage.py createsuperuser

## Run django with remote Postgres
kubectl run django --image=django_app --image-pull-policy=Never --env="SECRET_KEY=<SECRET_KEY>" --env="DATABASE_URL=postgres://test_k8s:OwOtBep9Frut@<HOST_ADDRESS>:5432/test_k8s"

## Port-forward
kubectl port-forward pod/django 8000:80

##
[admin panel](http://127.0.0.1:8000)
