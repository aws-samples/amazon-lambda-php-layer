# Lambda Layer Builder
![PHP Runtime Lambda Layer Builder](https://github.com/aws-samples/amazon-lambda-php-layer/blob/main/assets/PHP-Runtime-Layer-Builder.png?raw=true)
Use this Cloudformation template to automatically build a PHP runtime layer with the desired PHP version and extensions. This template will give you these options to select from upon stack creation and will automatically create all necessary resources to download, configure, compile and deploy the PHP runtime in a Lambda Layer. After stack creation is successful, you can delete the stack and keep the newly created Lambda Layer.

**Steps**

1. Download `template.yaml` file from this repository.

2. Navigate to AWS Cloudformation using the Console or CLI and deploy a new stack using the downloaded template.

3. Select the desired options and deploy the stack.

4. It will take the stack 10-15 minutes to complete. Once completed successfully, you can delete the stack.

The last step indicates a successful creation of the desired PHP runtime and Lambda layer. Now you can navigate to Lambda Layers and you should see your newly created layer.

To test the layer, create a new Lambda function, add the newly created layer to the function with a file named `index.php` and paste the following sample code:


```php
<?php

function handler($event) {

    return [
        'statusCode' => 200,
        'body' => 'Hello world!'
    ]

}
```
Note: the file name and handler function name will need to match Lambda's handler configuration. For example, if the handler configuration is set to `hello.handler`, then your file should be named `hello.php` and the function should be named `handler()`.

If you have dependencies such as composer packages in your code, compress the `vendor/*` directory and upload it to Lambda as a new layer. Then add the layer to the same Lambda function and you can use it as follows:

```php
<?php

require '/opt/vendor/autoload.php';
// or if the dependencies are bundled with the function itself use: require __DIR__ . '/vendor/autoload.php';

function handler($event) {

    return [
        'statusCode' => 200,
        'body' => 'Hello world!'
    ]

}
```

Note: It is highly recommended to keep the dependencies folder in its own layer `i.g. vendor layer` to be shared across different functions and for a lighter function deployment.