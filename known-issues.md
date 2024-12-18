
# Known Issues

---
## `AttributeError('`np.Inf` was removed in the NumPy 2.0 release. Use `np.inf` instead.'`

- Error message : 

``` bash
hydra.errors.InstantiationException: Error in call to target 'pytorch_lightning.callbacks.model_checkpoint.ModelCheckpoint':
AttributeError('`np.Inf` was removed in the NumPy 2.0 release. Use `np.inf` instead.')
full_key: entrypoints[1].trainer.callbacks2
```

- Solution : Numpy must be downgraded to version minor than 2.0

``` bash
conda install 'numpy<2.0'
```

---
## `ImportError: /opt/conda/lib/python3.9/site-packages/torch/lib/libtorch_cpu.so: undefined symbol: iJIT_NotifyEvent`

- Cause : 

``` bash
The reason is that PyTorch was built against an old version of MKL distribution which contains this symbol. However, this symbol got removed in MKL 2024.1.
The PyTorch binary released via conda channel was linked to MKL dynamically, so you got this error.
The PyTorch binary released via pip (pip install) was linked to MKL statically. You can switch to the pip install one to get rid of this error with MKL 2024.1.
...
```

- Solution : mkl must be downgraded to version `2024.0`
``` bash
conda install mkl==2024.0
```

Source :

- [https://github.com/pytorch/pytorch/issues/123097](https://github.com/pytorch/pytorch/issues/123097)


---
## `ERROR: Unexpected bus error encountered in worker. This might be caused by insufficient shared memory (shm)`

- Full message :
- 
``` bash
python main.py xp=base
# ...
# Testing: 0it [00:00, ?it/s]ERROR: Unexpected bus error encountered in worker. This might be caused by insufficient shared memory (shm).
# Error executing job with overrides: ['xp=base']
# Error in call to target 'src.test.base_test':
# RuntimeError('DataLoader worker (pid(s) 2387) exited unexpectedly')
# full_key: entrypoints1
```

- Cause
When working with worker, shm memory is needed, to allow workers to share datas. 

Solution :

1. Set `num_workers` to `0`, in the experience file. So worker  will not be used. It can be slow.

``` bash
{batch_size: 16, num_workers: 0}
```
2. Update SHM memory in the system if it is possible. About 512k must be enough.

To show SHM, use the command :
``` bash
df -h /dev/shm
```

---
## OutOfMemoryError('CUDA out of memory ...

- Full message
``` bash
OutOfMemoryError('CUDA out of memory. Tried to allocate 1.65 GiB (GPU 0; 47.74 GiB total capacity; 41.57 GiB already allocated; 665.69 MiB free; 43.08 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF')
full_key: entrypoints1
```

- Solution : reduce the value of `batch_size` in the experience file.
``` bash
{batch_size: 4, num_workers: 1}
```

To show the GPU memory, use the command `nvidia-smi`command.



---
## `Index error ...` when running `turbidity_output_analysis.ipynb`

The interval is defined differently in the experiment configuration file and in the notebook.

- In the experience config file
``` yaml
      time: {_target_: builtins.slice,  _args_: ['2020-06-01', '2020-06-26']}
```

- In the Notebook `turbidity_output_analysis.ipynb`, CELL 6 :

``` yaml
start_date='2020-06-01'
end_date='2020-06-26'
```

