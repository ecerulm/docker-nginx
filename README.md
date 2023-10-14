https://hub.docker.com/_/nginx

# Create multi-architecture image (intel / Apple Silicon M1 / M2)

```
docker buildx create --platform linux/arm64,linux/arm/v8,linux/arm/v7,linux/amd64 --name intel_and_apple_silicon --driver docker-container
docker buildx use intel_and_apple_silicon
docker buildx build --push --builder  intel_and_apple_silicon --platform linux/arm64/v8,linux/amd64 --tag ecerulm/mynginx:latest .
```

The [Docker Hub page for repo](https://hub.docker.com/repository/docker/ecerulm/mynginx/tags?page=1&ordering=last_updated)
will show the tag `latest` contains architectures

- linux/amd64 (intel)
- linux/arm64 (which is equivalent to linux/arm64/v8 which is Apple Silicon M1, M1 Max, M2)

# Run

```
docker run -ti --rm -p 8080:80 ecerulm/mynginx:latest
```

```
open http://localhost:8080
curl http://localhost:8080
```

# References

- [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)
    - [EXPOSE](https://docs.docker.com/engine/reference/builder/#expose) 
- docker run [-p 8080:80](https://docs.docker.com/engine/reference/run/#expose-incoming-ports)
- https://www.macstadium.com/blog/building-docker-images-on-apple-silicon-with-buildx
- https://www.docker.com/blog/multi-arch-build-and-images-the-simple-way/