# postgres

### docker

start postgres container:
```bash
docker run -d \
  --name postgres \
  -e POSTGRES_PASSWORD=password \
  postgres
```

login to database:
```bash
docker exec -it postgres psql -U postgres
```
