# LibreOffice for AWS Lambda as a layer

> 95 MB LibreOffice to fit inside AWS Lambda Layer compressed with Brotli or gzip

Based on the [serverless-libreoffice](https://github.com/vladgolubev/serverless-libreoffice) project.

## Publishing as Kenja

First make sure to configure your AWS CLI v2 and access credentials, then you can proceed to publish the Lambda layer.

```
source libreoffice-brotli.env
sh publish.sh
```

```
source libreoffice-gz.env
sh publish.sh
```

## Getting Started

Click on Layers and choose "Add a layer", and "Provide a layer version ARN" and enter the following ARN.

```
arn:aws:lambda:us-east-1:764866452798:layer:libreoffice-brotli:1
```

See the table below for the list of supported regions and runtimes.

Works well with [aws-lambda-libreoffice npm package](https://github.com/shelfio/aws-lambda-libreoffice)

## What's inside this layer?

`libreoffice-brotli` layer contains `lo.tar.br` file which is [LibreOffice v6.4.0.1](https://github.com/vladgolubev/serverless-libreoffice/releases/tag/v6.4.0.1). Node.js has native Brotli unpacking support since version 10 so it's easy to unpack this file natively. Alternatively, you can use [aws-lambda-libreoffice npm package](https://github.com/shelfio/aws-lambda-libreoffice) to simplify this task.

`libreoffice-gzip` layer contains `lo.tar.gz` file which is [LibreOffice v6.4.0.1](https://github.com/vladgolubev/serverless-libreoffice/releases/tag/v6.4.0.1).

## How do I use this layer to launch LibreOffice?

If you don't use [aws-lambda-libreoffice npm package](https://github.com/shelfio/aws-lambda-libreoffice), then these steps are roughly what you need to do.

1. This layer just adds `/opt/lo.tar.br` or `/opt/lo.tar.gz` file to your Lambda runtime
2. Unpack `/opt/lo.tar.br` or `/opt/lo.tar.gz` file during Lambda execution into `/tmp` folder which has 512 MB of free space. Make sure to do this OUTSIDE function handler code.
   This is an expensive task, so better to make it once on a warm start.
3. LibreOffice binary will be located available at `/opt/instdir/program/soffice.bin`
4. Check out `/test/index.js` for CLI arguments needed to run LibreOffice to convert a `.txt` file to `.pdf` for more details

## Version ARNs

### LibreOffice v6.4.0.1 (Amazon Linux 2)

*THESE ARNs ARE ONLY FOR USE WITH KENJA SERVICES*

Works with the following [AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html) which run on Amazon Linux 2:

- nodejs16.x
- nodejs14.x
- nodejs12.x
- nodejs10.x
- python3.8
- java11

| AWS Region     | Layer ARN (brotli)                                                                                                                                    |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| ap-northeast-1 | `arn:aws:lambda:ap-northeast-1:691624214751:layer:libreoffice-brotli:2` or <br> `arn:aws:lambda:ap-northeast-1:691624214751:layer:libreoffice-gzip:1` |

## License

MIT © [Shelf](https://shelf.io), [Kenja K.K.](https://kenja.com)
