# MLRun ci-demo

[![CircleCI](https://circleci.com/gh/mlrun/ci-demo/tree/master.svg?style=svg)](https://circleci.com/gh/mlrun/ci-demo/tree/master)

### Demo ml function CI/CD with MLRun and CircleCI

in order to add automated CI to ML functions you need to register your repo in [CircleCI](https://circleci.com/) and add the following YAML file to the `.circleci/config.yml` path.

You can also add a badge to your project like the one above, check the source of this MD file to see how

```yaml
version: 2
jobs:
  build:
    docker: 
      - image: python:3.6
    steps:
      - checkout
      - run: pip install mlrun
      - run: mlrun run --handler my_func --param-file params.csv --dump myfunc.py
```

The YAML instructs CircleCI to run a job every time you commit code to the branch, the Job will do the following:

1. Load a docker image (specified) and pull the code into it
2. Install MLRun package 
3. Test the function handler my_func in myfunc.py

> Note: it will run multiple tests, each test will use a set of parameters (a line) from the specified parameter file, at the end it will print (`--dump`) the run results as YAML
