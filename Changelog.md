# Changelog

## 2.6.1 - (2022-01-25)

- Fix a security issue with [CVE-2022-0235](https://github.com/advisories/GHSA-r683-j2x4-v87g) by upgrade [node-fetch](https://www.npmjs.com/package/node-fetch) (PR [459](https://github.com/Azure/ms-rest-js/pull/459))

## 2.6.0 - (2021-08-18)

- Added a new property `baseUri` on the `ServiceClientOptions` that is then used to initialize the corresponding `baseUri` protected property on the `ServiceClient`.
  - For `baseUri` that happen to be known Azure resource manager endpoints, this allows the instantiating of the `AzureIdentityCredentialAdapter` class with the right scope when a user constructs a `ServiceClient` with a `TokenCredential`. Resolves https://github.com/Azure/azure-sdk-for-js/issues/15945

## 2.5.3 - (2021-07-12)
- Updated the dependency on the uuid package to v8 (PR [456](https://github.com/Azure/ms-rest-js/pull/456))

## 2.5.2 - (2021-06-15)
- Fixed an issue where `proxySettings` does not work when there is username but no password (PR [453](https://github.com/Azure/ms-rest-js/pull/453))

## 2.5.1 - (2021-06-07)
- [BugFix] Array flattening in deserializer loses previously de-serialized attributes (PR [#451](https://github.com/Azure/ms-rest-js/pull/451))

## 2.5.0 - (2021-05-10)

- Add WebResource.redirectLimit: Limit the number of redirects followed for this request. If set to 0, redirects will not be followed.
- Port changes to redirect policy from [azure-sdk-for-js](https://github.com/Azure/azure-sdk-for-js/pull/11863/files]

## 2.4.1 - (2021-05-05)

- Use `self` instead of `window` in order to support web workers.

## 2.4.0 - 2021-04-19

- Expose `AzureIdentityCredentialAdapter` in the public API to enable users of this package make use of credentials from `@azure/identity`.

## 2.3.0 - 2021-03-29

- Moving @types dependencies into devdependencies
- Add NO_PROXY and ALL_PROXY support.
- Add username/password support in proxy url string.
- Update `WebResource.prepare()` to also copy `streamResponseBody`.

## 2.2.3 - 2021-02-10

- Dependent projects of @azure/ms-rest-js no longer need to have a dev dependency on @types/tunnel.

## 2.2.2 - 2021-02-09

- Port fix for nextLink issue from core-http (PR [#426](https://github.com/Azure/ms-rest-js/pull/426))
- Fix abort signal event handler memory leak (PR [#425](https://github.com/Azure/ms-rest-js/pull/425))
- Rework the use of `lib: ["dom"]` so consumers of this package don't need it in their tsconfig. Fixes (Issue [#367](https://github.com/Azure/ms-rest-js/issues/367))

## 2.2.1 - 2021-02-05

- Fix issue of `SystemErrorRetryPolicy` didn't retry on errors (Issue [#412](https://github.com/Azure/ms-rest-js/issues/412))
- `ThrottlingRetryPolicy` now keep retrying on 429 responses up to a limit. Fixes (Issue [#394](https://github.com/Azure/ms-rest-js/issues/394))
- The global `fetch()` is no longer overridden by node-fetch. Fixes (Issue [#383](https://github.com/Azure/ms-rest-js/issues/383))

## 2.2.0 - 2021-01-26

- Add support for @azure/core-auth's TokenCredential (PR [#410](https://github.com/Azure/ms-rest-js/pull/410))
- Allow = character in parameter value (PR [#408](https://github.com/Azure/ms-rest-js/pull/408))

## 2.1.0 - 2020-10-08

- Add support for custom http/https agent (PR [#403](https://github.com/Azure/ms-rest-js/pull/403))
- Fix WebResource clone to include extra settings (Issue [#405](https://github.com/Azure/ms-rest-js/issue/403))

## 2.0.8 - 2020-07-23

- [BugFix] - Fixed loading of proxyPolicy.browser.js in the HTML files.(PR [#397](https://github.com/Azure/ms-rest-js/pull/397))

## 2.0.7 - 2020-04-30

- Fixes encoding query parameters in an array before joining them.(PR [#382](https://github.com/Azure/ms-rest-js/pull/382))
- Replace public usage of `RequestPolicyOptions` to an interface `RequestPolicyOptionsLike` to avoid compatibility issues with private members.
- Fix issue with null/undefined values in array and tabs/space delimiter arrays during sendOperationRequest. [PR #390](https://github.com/Azure/ms-rest-js/pull/390)
- Fix in flattenResponse when expecting an array, checking for parsedBody to be an array before proceeding with flattening. (PR [#385](https://github.com/Azure/ms-rest-js/pull/385))

## 2.0.6 - 2020-04-15

- A new interface `WebResourceLike` was introduced to avoid a direct dependency on the class `WebResource` in public interfaces. `HttpHeadersLike` was also added to replace references to `HttpHeaders`. This change was added to improve compatibility between `@azure/core-http` and `@azure/ms-rest-nodeauth`.

## 2.0.5 - 2020-01-07

- Fix node-fetch bundling when using Webpack (PR [#376](https://github.com/Azure/ms-rest-js/pull/376)).

## 2.0.4 - 2019-07-30

- Ensure that a primitive type (string, number, boolean, null, undefined) response body with or without a `bodyMapper` is not flattened.

## 2.0.3 - 2019-07-11

- Added support to not send default values while sending the request.
- Added support to populate entities with it's default value if it is present in the mapper while deserializing the response.
- During deserialization, if the service does not provide the discriminator property then we set it. While setting the discriminator property, we compare model property name and the `clientName` of the `polymorphicDiscriminator` instead of the `serializedName` of the `polymorphicDiscriminator`.
- Added tests for serializing and deserializing additional properties.

## 2.0.2 - 2019-07-08

- Updated `cookieJar.setCookie()` with `{ ignoreError: true }` for `NodeFetchHttpClient`. This should silently ignore things like parse errors and invalid domains. This should resolve issues where customers using the `@azure/arm-appservice` package get an error due to mismatch in the domain [Azure/azure-sdk-for-js#1008](https://github.com/Azure/azure-sdk-for-js/issues/1008). This behavior makes it consistent with the old package [azure-arm-website](https://www.npmjs.com/package/azure-arm-website) which depends on the runtime [ms-rest](https://www.npmjs.com/package/ms-rest) that depends on the [request](https://www.npmjs.com/package/request) library which uses the [tough-cookie](https://www.npmjs.com/package/tough-cookie) package in `{ looseMode: true }` by [default](https://github.com/request/request/blob/536f0e76b249e4545c3ba2ac75e643146ebf3824/lib/cookies.js#L21) with `{ ignoreError: true }` as can be seen [here](https://github.com/request/request/blob/df346d8531ac4b8c360df301f228d5767d0e374e/request.js#L969).

## 2.0.1 - 2019-06-26

- Updated tests to include Pattern constraint

## 2.0.0 - 2019-06-21

- Change default HTTP client in Node.js environment from `axios`-based to `node-fetch`-based.
- Add `keepAlive` option to `WebResource` which sets proper header in Node.js HTTP client.
- **Breaking changes**:
  - AbortController
    - added required `dispatchEvent` method
    - added required (or null) `onabort` method
    - enforce type `Event` for `ev` parameter in `listener` in `addEventListener` and `removeEventListener`

## 1.8.13 - 2019-06-12

- Added DomainCredentials class for providing credentials to publish to an Azure EventGrid domain.

## 1.8.12 - 2019-06-07

- Added back the workaround of uppercasing method names otherwise axios causes issues with signing requests for storage data plane libraries.

## 1.8.11 - 2019-06-06

- Moved testing dependent projects from a script to Azure Devops Pipeline

## 1.8.10 - 2019-06-05

- `axios` changed the way it treats properties of the request config in `0.19.0`. Previously we were setting `trasnformResponse` to `undefined`. This would indicate `axios` to not transform (`JSON.parse()`) the response body. In `0.19.0`, they are setting the default response transformer if transformResponse is set to `undefined`. This breaks our pasrsing logic where we are doing `JSON.parse()` on `operationResponse.bodyAsText`. Moreover, we are exposing the `bodyAsText` property in the generated clients.
  Not populating this property or setting the value of this property to a parsed JSON would be a breaking change for our users.
  Hence we are setting the `transformResponse` property in the request config to an indentity function that returns the response body as-is.

## 1.8.9 - 2019-06-04

- Added build job to CI pipeline

## 1.8.8 - 2019-06-03

- Fixed vulnerabilities by bumping `axios` to `^0.19.0`.
- New version of axios fixed some issues hence removed one of the workarounds of uppercasing method names while following redirects [axios PR](https://github.com/axios/axios/pull/1758).

## 1.8.7 - 2019-05-16

- Fixed issue [#347](https://github.com/Azure/ms-rest-js/issues/347), [#348](https://github.com/Azure/ms-rest-js/issues/348) in PR [#349](https://github.com/Azure/ms-rest-js/pull/349)

## 1.8.6 - 2019-05-10

- Added script to run tests on dependent projects [#345](https://github.com/Azure/ms-rest-js/pull/345)

## 1.8.4 - 2019-05-07

- Fixed incorrect undefined check in Axios client [62b65d](https://github.com/Azure/ms-rest-js/commit/ea7ceb86f1e6e6f7879e7e7ddfe791113762b65d#diff-b9cfc7f2cdf78a7f4b91a753d10865a2)
- Added TSLint check. Fix TSLint errors [#344](https://github.com/Azure/ms-rest-js/pull/344)

## 1.8.2 - 2019-04-25

- Fixed http over https bug [#341](https://github.com/Azure/ms-rest-js/pull/341)

## 1.8.1 - 2019-04-01

- Fixed serialization issue when required object is empty [#337](https://github.com/Azure/ms-rest-js/pull/337)

## 1.8.0 - 2019-03-18

- Added exports to several request policy factory methods [#336](https://github.com/Azure/ms-rest-js/pull/336)

## 1.7.0 - 2019-02-11

- Added userAgentHeaderName to ServiceClientOptions [#330](https://github.com/Azure/ms-rest-js/pull/330)

## 1.6.0 - 2019-01-30

- Fixed including proxy policy in browser [0c552f](https://github.com/Azure/ms-rest-js/commit/fafa26180e591db43d43c9cf0c7e93c8030c552f#diff-b9cfc7f2cdf78a7f4b91a753d10865a2)

## 1.5.3 - 2019-01-25

- Brought Axios interceptors back [c33602](https://github.com/Azure/ms-rest-js/commit/c1742fe6a80ed9b794115362633e0a8307c33602#diff-b9cfc7f2cdf78a7f4b91a753d10865a2)

## 1.5.2 - 2019-01-25

- Added HTTP(S) over HTTP(S) proxy support [2b1844](https://github.com/Azure/ms-rest-js/commit/1ee5a40d5016e286a7492c8cbd7b08d5c92b1844#diff-b9cfc7f2cdf78a7f4b91a753d10865a2)
- Added `@types/tunnel` [0865a2](https://github.com/Azure/ms-rest-js/commit/7a9b496d04294446f940f1549fb0a44dd9b94c01#diff-b9cfc7f2cdf78a7f4b91a753d10865a2)

## 1.5.1 - 2019-01-22

- Fixed default HTTP client tests [c75b87](https://github.com/Azure/ms-rest-js/commit/4c2b1c5390deab989b5ec9cadb84891de9c75b87#diff-b9cfc7f2cdf78a7f4b91a753d10865a2)

## 1.5.0 - 2019-01-15

- Added support to specify proxy setting in ServiceClientOptions.

## 1.4.1 - 2019-01-15

- Movec browser-environment tests to Karma.

## 1.4.0 - 2019-10-15

- Allowed ServiceClientOptions.requestPolicyFactories to be a function.

## 1.3.0 - 2019-01-15

- Allowed ServiceClientOptions.userAgent property to be a function.

## 1.1.1 - 2018-11-13

- Improved debugging by adding rollup-plugin-sourcemaps.

## 1.1.0 - 2018-11-09

- Renamed NPM package to @azure/ms-rest-js.

## 1.0.0 - 2018-10-04

- Moved to Rollup for node and browser bundles
- Moved browser bundle from ./msRestBundle.js to ./dist/msRest.browser.js.

## 0.22.1 - 2018-09-27

- Added Authenticator type.

## 0.22.0 - 2018-09-05

- Added support for EventGrid TopicCredentials object.

## 0.21.0 - 2018-08-30

- Flatten response body properties, headers, etc. into one object for convenience

## 0.20.0 - 2018-08-24

- Fixed bug where operationSpec.baseUrl might get mutated
- Fixed some edge cases in response headers parsing in browser
- Refinements to support LRO work in ms-rest-azure-js

## 0.19.0 - 2018-08-22

- Improved type definitions of generated operation responses

## 0.18.0 - 2018-08-08

- Replaced RequestPolicyCreator function with RequestPolicyFactory interface with create() method.

## 0.17.0 - 2018-08-03

- Refactored mappers interfaces
- Added "sideEffects": false to package.json

## 0.16.0 - 2018-07-26

- Added timeout parameter to request options
- Call onDownload/UploadProgress callbacks in nodejs

## 0.15.0 - 2018-07-16

- Support x-nullable in Swagger
- Added architecture overview in docs/ folder
- Added withCredentials flag to request options

## 0.12.0, 0.13.0, 0.14.0 - 2018-06-25

- Moved header deserialization to runtime
- Using XhrHttpClient in browser
- Miscellaneous internal breaking changes

## 0.11.0 - 2018-06-21

- Support x-ms-header-collection-prefix in Swagger

## 0.10.0 - 2018-06-18

- Export RequestPolicyOptions

## 0.9.0 - 2018-06-14

- Fix base64 encoding in browser
- Add es6 module build
- withCredentials fixes
- Allow bundling individual operation groups instead of all operations

## 0.8.0 - 2018-05-31

- Add onDownloadProgress/onUploadProgress handlers for browser

## 0.7.0 - 2018-05-25

- Add parsed response headers support

## 0.6.0 - 2018-05-22

- Added URLBuilder to parse and build URLs
- Removed fetch responses from public APIs
- Added AbortSignal optional parameter to operations for cancellation

## 0.5.0 - 2018-05-08

- Replaced BaseFilter type with RequestPolicy.
- Removed ServiceClient.pipeline() in favor of ServiceClient.sendRequest().
- Started work on OperationSpecs to replace the imperative generated operations.

## 0.4.0 - 2018-05-03

- Added isomorphic-xml2js dependency to reduce browser package size
- Removed moment.js dependency, instead passing ISO 8601 strings for durations.

## 0.2.8 - 2018-04-02

- Relaxed validation for object types
- Relaxed handling of unrecognized polymorphic discriminator
- Added ApiKeyCredentials type

## 0.2.7 - 2018-03-23

- Updated moment to 2.21.0
- Added support to ensure that the provided Duration is a Duration like object. (based on ms-rest 2.3.2 in https://github.com/Azure/azure-sdk-for-node)

## 0.2.6 - 2018-02-22

- Added support for [de]serializing an "any" type (case when type is not present for an entity in the open api spec.). Resolves https://github.com/Azure/autorest/issues/2855
- Updated dependency versions

## 0.2.5 - 2018-01-25

- Compiled target to `ES5` for supporting IE11 #13.

## 0.2.4 - 2018-01-24

- Removed dependency on detect-node and added a utility method to detect whether the app is being executed in a node.js environment. Fixes #10.

## 0.2.3 - 2017-10-25

- We will return the actual response when the return type of a method in the generated code is `stream`. Hence, removing `bodyAsStream` property from `HttpOperationResponse`.

## 0.2.2 - 2017-10-17

- replacing eval by traversing recursively in the object.

## 0.2.1 - 2017-10-10

- moment version 2.19.0 has lot of issues. Hence fixing the dependency strictly to 2.18.1.

## 0.2.0 - 2017-10-10

- Reverting the change made in #2.

## 0.1.0 - 2017-09-16

- Initial version of ms-rest-js
  - Provides support for basic credentials
  - Supports serialization and deserialization of basic and complex types
  - Supports sending requests in the node environment and also in the browser
  - Builds the request pipeline by adding predefined filters
  - Provides mechanism to add custom flters in the pipeline
  - Provides a bundled file named [msRestBundle.js](./msRestBundle.js) that can be used in the browser
  - Please take a look at the [samples](./samples) directory for node and browser samples
