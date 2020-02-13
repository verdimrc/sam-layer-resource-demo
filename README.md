# sam-app

This is a minimum SAM template to demonstrate the behavior of layer resource, `sam local ...`, and `sam deploy`.

In summary:

1. you must have `pip install -t dependencies/python dependencies/python/requirements.txt`

2. `sam local ...` will work, because it simply mounts `dependencies/python` into the local container. See [this](https://github.com/awslabs/aws-sam-cli/issues/1481#issuecomment-546957976) and [this](https://github.com/awslabs/aws-sam-cli/issues/756#issuecomment-493143635) for the implementation details of sam.

3. `sam deploy ...` will create a .zip file of the layers.

   **NOTE**: this restricts you to run `sam deploy ...` only on a Linux machine.

   Otherwise, when you develop on a non-Linux machine, step 1 may pull in non-Linux packages (esp. if you deal alot with data-science-related packages like numpy, pandas, etc.). These non-Linux packages will be zipped and deployed as layer. This breaks the Lambda function when it attempts to use the modules inside the layer.
