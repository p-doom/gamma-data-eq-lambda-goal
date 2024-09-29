<!--
 Copyright 2024 Google LLC

 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at

      https://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.
 -->


[![Unit Tests](https://github.com/google/maxtext/actions/workflows/UnitTests.yml/badge.svg)](https://github.com/google/maxtext/actions/workflows/UnitTests.yml)

# Overview

 A first set of experiments on introspective exploration. 

This is a fork of [MaxText](https://github.com/AI-Hypercomputer/maxtext), Google's fastest and most feature-complete LLM implementation.

# Getting Started

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