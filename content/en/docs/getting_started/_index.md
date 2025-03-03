---
title: Getting started
linkTitle: Getting started
weight: 20
date: 2021-10-01
---

## Prerequisites

You should have npm (recommended minimum {{% variables/recommended_npm %}}), and Node.js (recommended minimum {{% variables/recommended_node %}}) installed.

{{% variables/apibuilder_prod_name %}} v4 maintains compatibility with a minimum of Node.js {{% variables/minimum_node %}}, however, using a version older than {{% variables/recommended_node %}} is not recommended. See the [Node.js support policy](/docs/nodejs_support_policy/) for more information.

### Minimum requirements

These are the absolute minimum requirements for running an {{% variables/apibuilder_prod_name %}} service. Memory and disk usage may fluctuate over time and between releases. Recommended system specs should be significantly higher to account for additional plugins, inbound requests and custom service logic.

|  | Development | Production |
| --- | --- | --- |
| HDD | 110MB | 80MB |
| RAM | 45MB | 40MB |

## Getting started

This section describes installing the Axway command line interface (CLI) and the {{% variables/apibuilder_prod_name %}} CLI. The {{% variables/apibuilder_prod_name %}} CLI is installed using the Axway CLI. We first describe how to install the Axway CLI, and then the {{% variables/apibuilder_prod_name %}} CLI.

### Install the Axway CLI globally

Refer to the [Axway CLI](https://docs.axway.com/bundle/axwaycli-open-docs/page/docs/index.html) documentation for more details.

```bash
// Install Axway CLI

npm install -g axway
```

Verify the Axway CLI installation by running the following command.

```bash
axway pm list
```

If you run into issues getting the Axway CLI working, see the [Axway CLI troubleshooting guide](https://docs.axway.com/bundle/axwaycli-open-docs/page/docs/troubleshooting/index.html). You may need to check that npm and Node.js were installed correctly.

### Install the {{% variables/apibuilder_prod_name %}} CLI

The {{% variables/apibuilder_prod_name %}} CLI is used to create new {{% variables/apibuilder_prod_name %}} projects and plugins.

Refer to [{{% variables/apibuilder_prod_name %}} CLI](/docs/developer_guide/cli/) documentation for more details.

```bash
// Install {{% variables/apibuilder_prod_name %}}

axway pm install @axway/amplify-api-builder-cli
```

### Create a new {{% variables/apibuilder_prod_name %}} project

Once {{% variables/apibuilder_prod_name %}} CLI is installed, you can use it to create a new project. In the following example, the CLI will create and initialize a project called `myproject` in the `./myproject` directory.

```bash
// Initialize a new project

axway builder init myproject
```

Then, start the {{% variables/apibuilder_prod_name %}} project.

```bash
// Run project

cd myproject
npm start
```

### Using version control

We recommend using version control for tracking changes. One popular version control solution is [git](https://git-scm.com/). {{% variables/apibuilder_prod_name %}} projects come with a .gitignore file which is used to ignore files and folders that should be downloaded or created as part of an install or build. These files and folders should not be versioned or distributed when sharing a project, as they can sometimes include sensitive information, or take up a large file size compared to the rest of the project (for example 150MB vs 30kb).

When cloning a project from elsewhere, you should ensure that all project dependencies, including {{% variables/apibuilder_prod_name %}} itself, are installed before you can start the service. From the project directory run:

```bash
// Install dependencies

npm ci
```

If you have issues running this command, it may be because the project is missing a package-lock.json file which specifies an exact dependency tree for reproducible installs. If this is the case, then run `npm install` instead.

### Updating {{% variables/apibuilder_prod_name %}}

New versions of {{% variables/apibuilder_prod_name %}} are released every 2 weeks, often containing important fixes and features. Each {{% variables/apibuilder_prod_name %}} project depends on it is own version of {{% variables/apibuilder_prod_name %}} which allows you to update your services individually.

To update {{% variables/apibuilder_prod_name %}} run the following command from your project directory. This will also update any additional dependencies in your project.

```bash
// Update dependencies

npm update
```

If you're going to be creating more {{% variables/apibuilder_prod_name %}} projects, it is important to use the latest {{% variables/apibuilder_prod_name %}} CLI so that your new projects use the latest template.

```bash
// Update Axway CLI and {{% variables/apibuilder_prod_name %}} CLI

npm install -g axway
axway pm update
```

For more information about fixes and features in new versions, see [{{% variables/apibuilder_prod_name %}} Release Notes](/docs/release_notes/). From time to time there will be changes to new projects and plugins. To keep your service in sync with these changes, see [{{% variables/apibuilder_prod_name %}} Updates](/docs/updates/).

## Introduction to the UI

Once your project is running, point your browser to `http://localhost:8080/console` to access the {{% variables/apibuilder_prod_name %}} user interface (UI) console.

Upon reviewing the {{% variables/apibuilder_prod_name %}} console, you can navigate to the following items.

|     |     |     |
| --- | --- | --- |
| ![summary_%281%29](/Images/summary_(1).png) | **Summary** | Your application's admin home page. |
| ![api](/Images/api.png) | **API Doc & Test** | Auto-generated documentation about your [API endpoints](/docs/developer_guide/flows/manage_endpoints/). Provides help for the client application to access your application. |
| ![image2021-1-12_10_21_51](/Images/image2021_1_12_10_21_51.png) | **Flows** | Lists [flows](/docs/developer_guide/flows/) that are part of your service and lets you [manage them](/docs/developer_guide/flows/manage_flows/). |
| ![models](/Images/models.png) | **Models** | Interface to help you build [models](/docs/developer_guide/models/). A model represents data stored from another source. |
| ![configuration](/Images/configuration.png) | **Configuration** | Lists [configuration](/docs/developer_guide/project/configuration/project_configuration/) files that you can modify and save within a browser. |
| ![credentials](/Images/credentials.png) | **Credentials** | Lists the currently configured [credentials](/docs/developer_guide/credentials/). |
| ![connectors](/Images/connectors.png) | **Plugins** | Lists available and installed [plugins](/docs/developer_guide/plugins/) to extend the core functionality of {{% variables/apibuilder_prod_name %}}, and that can be used to connect to different data sources and services or enhance the Flow editor. |
| ![View_Documentation](/Images/view_documentation.png) | **View Documentation** | Links to the Axway documentation for {{% variables/apibuilder_prod_name %}}. |
| ![image2019-8-6_12_9_34](/Images/image2019_8_6_12_9_34.png) | **Sidebar toggle** | Toggles the width of the sidebar. |

To quickly navigate to the **Summary** tab, click on the Axway icon or click on {{% variables/apibuilder_prod_name %}}.

## Advanced startup

You can choose which configuration values you want to be configurable from the environment by explicitly setting them in your `conf/default.js` using `process.env`. For example, to make the log level configurable, you could do:

```javascript
// Example environmental configuration variables

// Log level of the main logger
logLevel: process.env.LOG_LEVEL || 'debug',
```

This allows you to create containers for your application that can be configured when the container is started. The PORT is already environmentalized, so if you wish to launch {{% variables/apibuilder_prod_name %}} on a different port, you can set PORT as an environment variable. For example, on unix:

```bash
// Change port via env

// The port for the UI
$ PORT=8000 npm start
```

However, we recommend that you do not change the environmentalized port configuration in `conf/default.js` as this value is used when using Docker containers.

[Environmentalization guide](https://docs.axway.com/bundle/api-builder-security-guide/page/environmentalization.html) explains how to quickly set values to the environment variables referred to in the configuration files so they can be used during the development of the service.

## Further reading

Once you are familiar with startup and the UI, be sure to read the [Best Practices](/docs/best_practices/) guide as it will help guide your next phase of development.
