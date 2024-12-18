# List of Environment that has been validated 

---
## Python 3.11.10, CUDA 12.4.1, pytorch 2.5.1 with inseefrlab Docker image

- Docker image `inseefrlab/onyxia-jupyter-pytorch:py3.11.10-gpu`
```bash
docker run -it --rm --name 4dvarnet --gpus 0 -p 8888:8888 inseefrlab/onyxia-jupyter-pytorch:py3.11.10-gpu
``` 
- Python 3.11.10
- Environment.yaml file
``` yaml
  ...
  - pytorch::pytorch
  - pytorch::pytorch-cuda
  - pytorch-lightning
```

| Package           | Version |
| ----------------- | ------- |
| CUDA              |  12.4.1 |
| pytorch           |   2.5.1 |
| pytorch-cuda      |    12.4 |
| pytorch-lightning |   2.4.0 |
| torchaudio        |   2.5.1 |
| torchtriton       |   3.1.0 |
| torchvision       |  0.20.1 |



