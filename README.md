## Hasura GraphQL engine

Hasura is an open source engine that connects to your databases & microservices and auto-generates a production-ready GraphQL backend.

<img src=pics/hasura.png />

### Run Hasura GraphQL engine & Postgres
```bash
$ docker-compose up

Creating network "hasura-postgre-graphql_default" with the default driver
Creating hasura-postgre-graphql_postgres_1 ... done
Creating hasura-postgre-graphql_adminer_1        ... done
Creating hasura-postgre-graphql_graphql-engine_1 ... done

#Check if the containers are running
$ docker ps

CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS                  PORTS                    NAMES
636cf8ab4f9c        adminer                        "entrypoint.sh docke…"   10 seconds ago      Up 8 seconds            0.0.0.0:8082->8080/tcp   hasura-postgre-graphql_adminer_1
64c1dba7fe4f        hasura/graphql-engine:v1.1.0   "graphql-engine serve"   10 seconds ago      Up Less than a second   0.0.0.0:8080->8080/tcp   hasura-postgre-graphql_graphql-engine_1
89c1ae24249b        postgres:12                    "docker-entrypoint.s…"   15 seconds ago      Up 10 seconds           5432/tcp                 hasura-postgre-graphql_postgres_1

```

### `Northwind` sample database
Database contains the sales data for Northwind Traders, a fictitious specialty foods export-import company.

<img src=pics/ER.png />

### Adminer
Adminer (formerly phpMinAdmin) is a full-featured database management tool written in PHP. We will use it for postgres db management.

Access here: `http://localhost:8082/`

<img src=pics/adminer.png />

<img src=pics/adminer_home.png />

### Hasura console
Access here: `http://localhost:8080/console`

<img src=pics/hasura_login.png />

<img src=pics/hasura_home.png />

- GraphQL Query
  
```graphql
query MyQuery {
  products(where: {supplier: {city: {_eq: "Tokyo"}}}) {
    category_id
    quantity_per_unit
    reorder_level
    supplier_id
    unit_price
    units_in_stock
    units_on_order
  }
}
```

- Result

```json
{
  "data": {
    "products": [
      {
        "category_id": 6,
        "quantity_per_unit": "18 - 500 g pkgs.",
        "reorder_level": 0,
        "supplier_id": 4,
        "unit_price": 97,
        "units_in_stock": 29,
        "units_on_order": 0
      },
      {
        "category_id": 8,
        "quantity_per_unit": "12 - 200 ml jars",
        "reorder_level": 0,
        "supplier_id": 4,
        "unit_price": 31,
        "units_in_stock": 31,
        "units_on_order": 0
      },
      {
        "category_id": 7,
        "quantity_per_unit": "5 kg pkg.",
        "reorder_level": 5,
        "supplier_id": 4,
        "unit_price": 10,
        "units_in_stock": 4,
        "units_on_order": 20
      }
    ]
  }
}
```

### Stop docker-compose
  
Stop the server that was launched by docker compose up via Ctrl-C, then remove the containers via:

```bash
$ docker-compose down
```