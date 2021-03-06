# serverless-finch

[![npm](https://img.shields.io/npm/dm/serverless-finch.svg)](https://www.npmjs.com/package/serverless-finch)
[![npm](https://img.shields.io/npm/v/serverless-finch.svg)](https://www.npmjs.com/package/serverless-finch)
[![license](https://img.shields.io/github/license/fernando-mc/serverless-finch.svg)](https://github.com/fernando-mc/serverless-finch/blob/master/LICENSE)

A Serverless Framework plugin for deployment of static website assests of your Serverless project to AWS S3.

## Installation

```
npm install --save serverless-finch
```

## Usage

**First,** update your `serverless.yml` by adding the following:

```yaml
plugins:
  - serverless-finch

custom:
  client:
    bucketName: [unique-s3-bucketname] # (see Configuration Parameters below)
    # [other configuration parameters] (see Configuration Parameters below)
```

**NOTE:** *For full example configurations, please refer to the [examples](examples) folder.*

**Second**, Create a website folder in the root directory of your Serverless project. This is where your distribution-ready website should live. By default the plugin expects the files to live in a folder called `client/dist`. But this is configurable with the `distributionFolder` option (see the [Configuration Parameters](#configuration-parameters) below).

The plugin uploads the entire `distributionFolder` to S3 and configures the bucket to host the website and make it publicly available, also setting other options based the [Configuration Parameters](#configuration-parameters) specified in `serverless.yml`.

To test the plugin initially you can copy/run the following commands in the root directory of your Serverless project to get a quick sample website for deployment:

```bash
mkdir -p client/dist
touch client/dist/index.html
touch client/dist/error.html
echo "Go Serverless" >> client/dist/index.html
echo "error page" >> client/dist/error.html
```

**Third**, run the plugin, and visit your new website!

```
serverless client deploy [--stage $STAGE] [--region $REGION]
```

The plugin should output the location of your newly deployed static site to the console.

**WARNING:** The plugin will overwrite any data you have in the bucket name you set above if it already exists.

If later on you want to take down the website you can use:

```bash
serverless client remove
```

### Configuration Parameters

**bucketName**

_required_

```yaml
custom:
  client:
    bucketName: [unique-s3-bucketname]
```

Use this parameter to specify a unique name for the S3 bucket that your files will be uploaded to.

---

**distributionFolder**

_optional_, default: `client/dist`

```yaml
custom:
  client:
    ...
    distributionFolder: [path/to/files]
    ...
```

Use this parameter to specify the path that contains your website files to be uploaded. This path is relative to the path that your `serverless.yaml` configuration files resides in.

---

**indexDocument**

_optional_, default: `index.html`

```yaml
custom:
  client:
    ...
    indexDocument: [file-name.ext]
    ...
```

The name of your index document inside your `distributionFolder`. This is the file that will be served to a client visiting the base URL for your website.

---

**errorDocument**

_optional_, default: `error.html`

```yaml
custom:
  client:
    ...
    errorDocument: [file-name.ext]
    ...
```

The name of your error document inside your `distributionFolder`. This is the file that will be served to a client if their initial request returns an error (e.g. 404). For an SPA, you may want to set this to the same document specified in `indexDocument` so that all requests are redirected to your index document and routing can be handled on the client side by your SPA.

---

### Command-line Parameters

No command-line parameters exist at this time.

## Contributing

For guidelines on contributing to the project, please refer to our [Contributing](docs/CONTRIBUTING.md) page. 

## Release Notes

### v1.4.\*
- Added the ability to set custom index and error documents. ([Pull 20](https://github.com/fernando-mc/serverless-finch/pull/20) - [evanseeds](https://github.com/evanseeds))

### v1.3.\*
- Added the ability to set a `distributionFolder` configuration value. This enables you to upload your website files from a custom directory ([Pull 12](https://github.com/fernando-mc/serverless-finch/pull/12) - [pradel](https://github.com/pradel))
- Updated the URL to the official static website endpoint URL ([Pull 13](https://github.com/fernando-mc/serverless-finch/pull/13) - [amsross](https://github.com/amsross))
- Added a new AWS region ([Pull 14](https://github.com/fernando-mc/serverless-finch/pull/14) - [daguix](https://github.com/daguix))
- Fixed an issue with resolving serverless variables ([Pull 18](https://github.com/fernando-mc/serverless-finch/pull/18) - [shentonfreude](https://github.com/shentonfreude))

### v1.2.\*
- Added the `remove` option to tear down what you deploy. ([Pull 10](https://github.com/fernando-mc/serverless-finch/pull/10) thanks to [redroot](https://github.com/redroot))
- Fixed automated builds for the project (no functional differences)

## Maintainers
- **You** - If you're interested in having a more active role in development and becoming a maintainer [get in touch](https://www.fernandomc.com/contact/).
- Fernando Medina Corey - [fernando-mc](https://github.com/fernando-mc)

## Contributors
- [redroot](https://github.com/redroot)
- [amsross](https://github.com/amsross)
- [pradel](https://github.com/pradel)
- [daguix](https://github.com/daguix)
- [shentonfreude](https://github.com/shentonfreude)
- [evanseeds](https://github.com/evanseeds)

Forked from the [**serverless-client-s3**](https://github.com/serverless/serverless-client-s3/)
