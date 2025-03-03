---
title: Compose flow-node
linkTitle: Compose flow-node
weight: 40
date: 2021-10-01
---

The Compose (doT) flow-node methods, parameters, and outputs are described in the following sections. The Compose flow-node is created when npm installs the `@axway/api-builder-plugin-fn-dot` plugin. The Compose flow-node plugin is included in the default application, but it can be removed. For additional doT flow-node information, refer to [doT flow-node](/docs/developer_guide/flows/flow_nodes/dot_flow_node/).

{{% alert title="Note" color="primary" %}}Installing the Compose (doT) flow-node module may report a security vulnerability with doT. This is because doT templates can be used to execute malicious JavaScript.

**Templates should never come from untrusted sources**. If you trust all the templates that you use, then you can safely ignore the vulnerability and continue to use this plugin.

This plugin is no longer bundled with new {{% variables/apibuilder_prod_name %}} projects. We suggest using [JavaScript flow-node](/docs/developer_guide/flows/flow_nodes/javascript_flow_node) instead of the `formatObject` method, or [Mustache flow-node](/docs/developer_guide/flows/flow_nodes/mustache_flow_node) instead of `formatString`.{{% /alert %}}

## Methods

The default methods for a Compose flow-node are:

* `Format object` - Compose an object by evaluating a template. The evaluated template is JSON parsed and so must be a valid JSON encoded string. For additional information, see [https://olado.github.io/dot](https://olado.github.io/dot).
* `Format string` - Compose a string by evaluating a template. For additional information, see [https://olado.github.io/dot](https://olado.github.io/dot).

## Parameters

The Compose flow-node parameters are described in the following sections.

### Format object parameters

The `Format object` method parameters are:

| Parameter | Type | Description | Configuration selection |
| --- | --- | --- | --- |
| data | object | The data to evaluate the template with. Use $ to access the entire context. | Selector, Object |
| template | string | The doT template. | Selector, String |

### Format string parameters

The `Format string` method parameters are:

| Parameter | Type | Description | Configuration selection |
| --- | --- | --- | --- |
| data | object | The data to evaluate the template with. Use $ to access the entire context. | Selector, Object |
| template | string | The doT template. | Selector, String |

## Outputs

The Compose flow-node outputs are described in the following sections.

### Format object outputs

The `Format object` method outputs are:

| Output | Type | Description | Save output value as: |
| --- | --- | --- | --- |
| Next | any | \- | $.value |
| Error | any | This output is triggered if the evaluated template is not a valid JSON string. The output value is the error object. | $.error |

### Format string outputs

The `Format string` method outputs are:

| Output | Type | Description | Save output value as: |
| --- | --- | --- | --- |
| Next | any | \- | $.value |
| Error | any | This output is triggered if the evaluated template is not valid. The output value is the error object. | $.error |
