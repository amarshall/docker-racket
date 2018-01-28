# Racket for Docker

This is [Racket](https://racket-lang.org/) for Docker.

## Usage

It’s best to use this in a two-stage build pipeline for minimal image size:

```Dockerfile
FROM amarshall/racket AS compiler

WORKDIR /root
COPY main.rkt .
RUN raco exe -o main main.rkt
RUN raco distribute dist main

FROM debian:stable-slim
COPY --from=compiler /root/dist /opt
CMD ["/opt/bin/main"]
```
