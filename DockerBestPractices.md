# Docker Best Practices

## Use Offcial Docker Images as Base Image
- FROM ubuntu (X)
- FROM node (0)

## do not use latest tag (Use Spectific Image Versions)
- FROM node (:latest) (X)
- FROM node:17.0.1 (O)

## Use small-sized Officaln Images
- FROM node:17.0.1 (X)
- FROM node:17.0.1-alpine (O)

## Optimize Caching Image Layers
- small change -> large change

## Use .dockerignore

## multi-stage builds
```dockerfile
# build stage
FROM maven AS build
WORKDIR /app
COPY myapp /app
RUN mvn package

# run stage
FROM build
COPY --from=build /app/target/file.war /usr/local/tomcat/web.war
```
```
docker build . -t multi-stage-example:v1 --target=build
```

## Use the Least Privileged User
```dockerfile
RUN groupadd -r tom && useradd -g tom tom
RUN chown -R tom:tom /app
USER tom
CMD node index.js
```

## Scan Your Images forn Vulnerabilities
```bash
docker scan myapp:1.0
```

## Use non-root user to run the containers
## Use .dockerignore file
## Use BuildKit (export DOCKER_BUILDKIT=1)
## Use hadolint (or any other linter)
## Use analysis tools (dive, skopeo)
## Use multi staged builds
## Base images: slim | alpine | distroless
## Use image scanners (synk, anchore, jfrong xray)
