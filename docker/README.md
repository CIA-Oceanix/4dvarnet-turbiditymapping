# Docker image for 4DVarNet - Turbibity Mapping

---
## Build

Start the build

- Set the tag (do not use `latest` or `stable`)
```bash
export IMAGE_TAG=1.3
```
- Build the image
```bash
docker build \
  --progress=plain \
  --no-cache \
  -f docker/Dockerfile \
  -t ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:$IMAGE_TAG \
  .
```

---
## Test the image

- Start a container:
    - In console mode
```bash
docker run -it --rm --name turbiditymapping ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:$IMAGE_TAG bash
```
    - In graphical mode (jupyterlab)
```bash
docker run --rm -p 8888:8888 --name turbiditymapping-lab ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:$IMAGE_TAG
```
- Test : run the notebook `turbidity_output_analysis.ipynb` in graphical mode
- If needed, remove the container
    - In console mode
```bash
docker rm --force turbiditymapping
```
    - In graphical mode (jupyterlab)
```bash
docker rm --force turbiditymapping-lab
```

---
## Publish the image to the Github registry

```bash
docker push ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:$IMAGE_TAG
```

---
## Set the `latest` and `stable` versions

- stable
```bash
# Define TAG used for stable
export TAG_FOR_STABLE=1.3

# Pull image
docker pull ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:$TAG_FOR_STABLE
# Tag it as stable
docker tag ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:$TAG_FOR_STABLE ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:stable
# And push it
docker push ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:stable
```
- latest
```bash
# Define TAG used for latest 
export TAG_FOR_LATEST=0.1.0

# Pull image
docker pull ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:$TAG_FOR_LATEST
# Tag it as latest
docker tag ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:$TAG_FOR_LATEST ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:latest
# And push it
docker push ghcr.io/cia-oceanix/4dvarnet-turbiditymapping:latest
```