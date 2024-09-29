# Getting Started

We recommend starting with a single host first and then moving to multihost.

### Environment setup
We need to pin python to 3.10 since `tensorflow-text` does not seem to support `python 3.12`.

Contrary to the upstream repository, we use `uv`. This means, all you have to do is:
```
uv sync
```

[comment]: # TODO: check whether we should be running pre-commit in the gpu case

After installation is completed, run training with the command on synthetic data:

```
python3 MaxText/train.py MaxText/configs/base.yml \
  run_name=$YOUR_JOB_NAME \
  base_output_directory=gs://<my-bucket> \
  dataset_type=synthetic \
  steps=10  
```

3. If you want to decode, you can decode as follows.
```
python3 MaxText/decode.py MaxText/configs/base.yml \
  run_name=$YOUR_JOB_NAME \
  base_output_directory=gs://<my-bucket> \
  per_device_batch_size=1  
```

* If you see the following error when running inside a container, set a larger `--shm-size` (e.g. `--shm-size=1g`)
```
Failed to execute XLA Runtime executable: run time error: custom call 'xla.gpu.all_reduce' failed: external/xla/xla/service/gpu/nccl_utils.cc:297: NCCL operation ncclCommInitRank(&comm, nranks, id, rank) failed: unhandled cuda error (run with NCCL_DEBUG=INFO for details); current tracing scope: all-reduce-start.2; current profiling annotation: XlaModule:#hlo_module=jit__unnamed_wrapped_function_,program_id=7#.
```

## Getting Starting: Preflight Optimizations

Once you've gotten workloads running, there are important optimizations you might want to put on your cluster. Please check the doc [PREFLIGHT.md](https://github.com/google/maxtext/blob/main/PREFLIGHT.md)
