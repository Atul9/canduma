[![MIT license](http://img.shields.io/badge/license-MIT-brightgreen.svg)](http://opensource.org/licenses/MIT)
[![Status](https://img.shields.io/badge/build-passing-brightgreen)]()
[![Status](https://img.shields.io/badge/pull--request-open-blue)]()

# Canduma rust server boilerplate
`A Rust web server with GraphQL API, Diesel, PostgreSQL and JWT authentication.`

This repository contains boilerplate rust code for getting a GraphQL prototype with JWT up and running quickly.
 
It uses [actix-web](https://actix.rs/), [Juniper](https://graphql-rust.github.io/juniper/current/), 
[Diesel](http://diesel.rs/) and [jsonwebtoken](https://docs.rs/jsonwebtoken)

Your own pull requests are welcome!

## Benchmarks with insert into PostgreSQL
```shell script
▶ ./bombardier -c 125 -n 10000000 http://localhost:3000/graphql -k -f body --method=POST -H "Content-Type: application/json" -s    
Bombarding http://localhost:3000/graphql with 10000000 request(s) using 125 connection(s)

10000000 / 10000000 [===========================================================================] 100.00% 28777/s 5m47s
Done!
Statistics        Avg      Stdev        Max
  Reqs/sec     28788.66    2183.47   34605.95
  Latency        4.32ms   543.07us   110.95ms
  HTTP codes:
    1xx - 0, 2xx - 10000000, 3xx - 0, 4xx - 0, 5xx - 0
    others - 0
  Throughput:    20.75MB/s
```


## Collection of major crates used in Canduma
* actix - [link](https://actix.rs/)
* actix-web - [link](https://docs.rs/actix-web/)
* diesel - [link](http://diesel.rs/)
* juniper - [link](https://graphql-rust.github.io/juniper/current/)
* chrono - [link](https://docs.rs/chrono/)
* serde_json - [link](https://docs.serde.rs/serde_json/)
* argon2rs - [link](https://github.com/bryant/argon2rs)
* jsonwebtoken - [link](https://docs.rs/jsonwebtoken)

## Required
* [Rustup](https://rustup.rs/)
* Nightly Toolchain: `rustup default nightly`
* Diesel cli with postgres `cargo install diesel_cli --no-default-features --features "postgres"`
* PostgreSQL database server or use our docker-compose.yml (require docker)

## Getting Started
```sh
git clone https://github.com/clifinger/canduma.git
cd canduma
docker-compose up
cp .env.example .env
diesel setup --database-url='postgres://postgres:canduma@localhost/canduma'
diesel migration run
cargo run
```
## Test the GraphQL API with Insomnia
### Register
![Register with Insomnia](https://github.com/clifinger/canduma/blob/master/docs/images/insomnia-register.png?raw=true)

### Login
![Login with Insomnia](https://github.com/clifinger/canduma/blob/master/docs/images/insomnia-login.png?raw=true)

### Set Bearer JWT Token
![Set JWT Token with Insomnia](https://github.com/clifinger/canduma/blob/master/docs/images/insomnia-set-bearer.png?raw=true)

### Test authentication with JWT by getting all users
![Set Token with Insomnia](https://github.com/clifinger/canduma/blob/master/docs/images/insomnia-test-jwt-by-get-members.png?raw=true)

## Build release
```sh 
cargo build --release
cd target/release
./canduma
```