# postgres

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

cheatsheet
---|
https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546
https://www.postgresqltutorial.com/postgresql-cheat-sheet/

