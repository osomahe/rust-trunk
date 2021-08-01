# Rust + Trunk Docker image

This project provides docker image with rust and trunk install. It can be used to build yew application for nginx.

```
FROM osomahe/rust-trunk as builder

RUN mkdir /web
ADD Cargo.toml index.html Trunk.toml /web/
ADD src /web/src/
ADD static /web/static/
WORKDIR /web
RUN trunk build --release

FROM nginx:1.21-alpine

COPY nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /web/dist/ /usr/share/nginx/html/
```

