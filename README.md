# postgres

Install `psql`:
```bash
brew install libpq
echo 'export PATH="/opt/homebrew/opt/libpq/bin:$PATH"' >> ~/.zshrc
```

Deploy postgresql:
```bash
helm upgrade -i postgresql bitnami/postgresql \
  --version 16.0.0 \
  --set primary.service.type=LoadBalancer \
  --set auth.postgresPassword=postgres \
  --set auth.database=test
```

---

### OLD

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
  --set postgresql.replicaCount=3 \
  --set persistence.storageClass=openebs-hostpath
```

create a service with name `postgresql`:
```yaml
kubectl create -f - << EOF
apiVersion: v1
kind: Service
metadata:
  name: postgresql
  namespace: orc8r
spec:
  ports:
    - name: postgresql
      protocol: TCP
      port: 5432
      targetPort: postgresql
  selector:
    app.kubernetes.io/component: postgresql
    app.kubernetes.io/instance: postgresql-ha
    app.kubernetes.io/name: postgresql-ha
EOF
```

connect to magma database:
```bash
PGPASSWORD=postgres psql -U postgres -d magma
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

