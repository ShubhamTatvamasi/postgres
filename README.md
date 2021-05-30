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

cheatsheet https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546

