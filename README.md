# postgres

Install postgresql:
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update

helm upgrade -i postgresql bitnami/postgresql \
  --set postgresqlPassword=postgres \
  --set postgresqlDatabase=magma \
  --set persistence.storageClass=openebs-jiva-csi-default \
  --set replication.enabled=true \
  --set replication.readReplicas=2
```


Deploy Postgresql High Availability 
```bash
helm upgrade -i postgresql-ha bitnami/postgresql-ha \
  --set postgresql.password=postgres \
  --set postgresql.database=magma \
  --set postgresql.replicaCount=3
```

### docker

install psql:
```bash
sudo apt install postgresql-client
```

start postgres container:
```bash
docker run -d -p 5432:5432 \
  --name postgres \
  -e POSTGRES_PASSWORD=postgres \
  postgres
```

login to database:
```bash
docker exec -it postgres psql -U postgres
```

run pgadmin4:
```bash
docker run -p 80:80 \
    -e 'PGADMIN_DEFAULT_EMAIL=user@domain.com' \
    -e 'PGADMIN_DEFAULT_PASSWORD=SuperSecret' \
    -d dpage/pgadmin4
```

### kubernetes

create postgres pod on kubernetes:
```bash
kubectl run postgres --image=postgres \
  --env=POSTGRES_PASSWORD=postgres \
  --env=POSTGRES_DB=magma \
  --expose --port=5432
```


cheatsheet
---|
https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546
https://www.postgresqltutorial.com/postgresql-cheat-sheet/

