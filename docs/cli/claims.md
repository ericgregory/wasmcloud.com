---
title: "wash claims"
draft: false
sidebar_position: 5
description: "wash claims command reference"
---

Every component in a wasmCloud environment contains metadata which are called claims, in the form of JSON Web Tokens (JWTs).

`wash claims` helps generate, manage and view these JWTs for wasmCloud components.

The following are the subcommands available under `wash claims`.

- `inspect`
- `sign`
- `token`

## `inspect`

:::warning
This subcommand will be deprecated in future versions. Please use `wash inspect` instead.
:::

`wash inspect` helps you to examine the stored metadata of a wasmCloud component. `wash inspect` accepts the path to the wasmCloud component or provider and prints out the properties of that component.

#### Usage

```
➜ wash claims inspect wasmcloud.azurecr.io/echo:0.3.7


                               Echo - Module
  Account       ACOJJN6WUP4ODD75XEBKKTCCUJJCY5ZKQ56XVKYK4BEJWGVAOOQHZMCW
  Module        MBCFOPM6JW2APJLXJD3Z5O4CN7CPYJ2B4FTKLJUR5YR5MITIU7HD3WD5
  Expires                                                          never
  Can Be Used                                                immediately
  Version                                                      0.3.7 (4)
  Call Alias                                                   (Not set)
                                   Tags
  None


➜ wash claims inspect wasmcloud.azurecr.io/httpserver:0.19.1


                            HTTP Server - Provider Archive
  Account                   ACOJJN6WUP4ODD75XEBKKTCCUJJCY5ZKQ56XVKYK4BEJWGVAOOQHZMCW
  Service                   VAG3QITQQ2ODAOWB5TTQSDJ53XK3SHBEIFNK4AYJ5RKAX2UNSCAPHA5M
  Capability Contract ID                                        wasmcloud:httpserver
  Vendor                                                                   wasmCloud
  Version                                                                     0.17.0
  Revision                                                                         0
                            Supported Architecture Targets
  x86_64-macos
  armv7-linux
  aarch64-linux
  x86_64-windows
  x86_64-linux
  aarch64-macos

```

#### Options

`--jwt-only` Extract the raw JWT from the file and print to stdout

`--output` (Alias `-o`) Specify output format (text or json) [default: text]

`--digest` (Alias `-d`) Digest to verify artifact against (if OCI URL is provided for component)

`--experimental` Whether or not to enable experimental features [env: WASH_EXPERIMENTAL=]

`--allow-latest` Allow latest artifact tags (if OCI URL is provided for component)

`--user` (Alias `-u`) OCI username, if omitted anonymous authentication will be used [env: WASH_REG_USER]

`--password` (Alias `-p`) OCI password, if omitted anonymous authentication will be used [env: WASH_REG_PASSWORD]

`--insecure` Allow insecure (HTTP) registry connections

`--no-cache` skip the local OCI cache

## `sign`

`wash claims sign` assists you in signing a WebAssembly component with metadata about the component. Users may specify metadata such as expiration, tags, etc.

#### Usage

```
wash claims sign /path/to/wasm-module --name=component-name
```

#### Options

`--destination` (Alias `-d`) Destination for signed module. If this flag is not provided, the signed module will be placed in the same directory as the source with a "\_s" suffix

`--output` (Alias `-o`) Specify output format (text or json) [default: text]

`--experimental` Whether or not to enable experimental features [env: WASH_EXPERIMENTAL=]

`--msg` (Alias `-g`) Enable the Message broker standard capability

`--name` (Alias `-n`) A human-readable, descriptive name for the token

`--tag` (Alias `-t`) A list of arbitrary tags to be embedded in the token

`--prov` (Alias `-p`) Indicates whether the signed module is a capability provider instead of a component (the default is component)

`--rev` (Alias `-r`) Revision number

`--ver` (Alias `-v`) Human-readable version string

`--call-alias` (Alias `-a`) Developer or human friendly unique alias used for invoking a component, consisting of lowercase alphanumeric characters, underscores '\_' and slashes '/'

`--issuer` (Alias `-i`) Path to issuer seed key (account). If this flag is not provided, the will be sourced from $WASH_KEYS ($HOME/.wash/keys) or generated for you if it cannot be found [env: WASH_ISSUER_KEY]

`--subject` (Alias `-s`) Path to subject seed key (module). If this flag is not provided, the will be sourced from $WASH_KEYS ($HOME/.wash/keys) or generated for you if it cannot be found [env: WASH_SUBJECT_KEY]

`--directory` Location of key files for signing. Defaults to $WASH_KEYS ($HOME/.wash/keys) [env: WASH_KEYS]

`--expires` (Alias `-x`) Indicates the token expires in the given amount of days. If this option is left off, the token will never expire

`--nbf` (Alias `-b`) Not before days. Period in days that must elapse before this token is valid. If this option is left off, the token will be valid immediately

`--disable-keygen` Disables autogeneration of keys if seed(s) are not provided

## `token`

Using this subcommand, a user can generate signed JWTs for components, operators, accounts and providers by supplying basic token information, a signing seed key and metadata. Following are the subcommands available under token.

- `component`
- `operator`
- `account`
- `provider`

### `component`

Generate a signed JWT for a component

#### Usage

```
wash claims token component --name=example -k
```

#### Options

`--output` (Alias `-o`) Specify output format (text or json) [default: text]

`--experimental` Whether or not to enable experimental features [env: WASH_EXPERIMENTAL=]

`--msg` (Alias `-g`) Enable the Message broker standard capability

`--name` (Alias `-n`) A human-readable, descriptive name for the token

`--tag` (Alias `-t`) A list of arbitrary tags to be embedded in the token

`--prov` (Alias `-p`) Indicates whether the signed module is a capability provider instead of a component (the default is component)

`--rev` (Alias `-r`) Revision number

`--ver` (Alias `-v`) Human-readable version string

`--call-alias` (Alias `-a`) Developer or human friendly unique alias used for invoking a component, consisting of lowercase alphanumeric characters, underscores '\_' and slashes '/'

`--issuer` (Alias `-i`) Path to issuer seed key (account). If this flag is not provided, the will be sourced from $WASH_KEYS ($HOME/.wash/keys) or generated for you if it cannot be found [env: WASH_ISSUER_KEY]

`--subject` (Alias `-s`) Path to subject seed key (module). If this flag is not provided, the will be sourced from $WASH_KEYS ($HOME/.wash/keys) or generated for you if it cannot be found [env: WASH_SUBJECT_KEY]

`--directory` Location of key files for signing. Defaults to $WASH_KEYS ($HOME/.wash/keys) [env: WASH_KEYS]

`--expires` (Alias `-x`) Indicates the token expires in the given amount of days. If this option is left off, the token will never expire

`--nbf` (Alias `-b`) Not before days. Period in days that must elapse before this token is valid. If this option is left off, the token will be valid immediately

`--disable-keygen` Disables autogeneration of keys if seed(s) are not provided

### `operator`

Generate a signed JWT for an operator

#### Usage

```
wash claims token operator --name=example
```

#### Options

`--name` (Alias `-n`) A human-readable, descriptive name for the token

`--output` (Alias `-o`) Specify output format (text or json) [default: text]

`--experimental` Whether or not to enable experimental features [env: WASH_EXPERIMENTAL=]

`--issuer` (Alias `-i`) Path to issuer seed key (account). If this flag is not provided, the will be sourced from $WASH_KEYS ($HOME/.wash/keys) or generated for you if it cannot be found [env: WASH_ISSUER_KEY]

`--additional-key` (Alias `-a`) Additional keys to add to valid signers list Can either be seed value or path to seed file

`--directory` Location of key files for signing. Defaults to $WASH_KEYS ($HOME/.wash/keys) [env: WASH_KEYS]

`--expires` (Alias `-x`) Indicates the token expires in the given amount of days. If this option is left off, the token will never expire

`--nbf` (Alias `-b`) Not before days. Period in days that must elapse before this token is valid. If this option is left off, the token will be valid immediately

`--disable-keygen` Disables autogeneration of keys if seed(s) are not provided

### `account`

Generate a signed JWT for an account

#### Usage

```
wash claims token account --name=example
```

#### Options

`--name` (Alias `-n`) A human-readable, descriptive name for the token

`--output` (Alias `-o`) Specify output format (text or json) [default: text]

`--experimental` Whether or not to enable experimental features [env: WASH_EXPERIMENTAL=]

`--issuer` (Alias `-i`) Path to issuer seed key (account). If this flag is not provided, the will be sourced from $WASH_KEYS ($HOME/.wash/keys) or generated for you if it cannot be found [env: WASH_ISSUER_KEY]

`--subject` (Alias `-s`) Path to subject seed key (module). If this flag is not provided, the will be sourced from $WASH_KEYS ($HOME/.wash/keys) or generated for you if it cannot be found [env: WASH_SUBJECT_KEY]

`--additional-key` (Alias `-a`) Additional keys to add to valid signers list Can either be seed value or path to seed file

`--directory` Location of key files for signing. Defaults to $WASH_KEYS ($HOME/.wash/keys) [env: WASH_KEYS]

`--expires` (Alias `-x`) Indicates the token expires in the given amount of days. If this option is left off, the token will never expire

`--nbf` (Alias `-b`) Not before days. Period in days that must elapse before this token is valid. If this option is left off, the token will be valid immediately

`--disable-keygen` Disables autogeneration of keys if seed(s) are not provided

### `provider`

Generate a signed JWT for a capability provider

#### Usage

```
wash claims token provider --name=example --vendor=vendor-name
```

#### Options

`--name` (Alias `-n`) A human-readable, descriptive name for the token

`--output` (Alias `-o`) Specify output format (text or json) [default: text]

`--experimental` Whether or not to enable experimental features [env: WASH_EXPERIMENTAL=]

`--vendor` (Alias `-v`) A human-readable string identifying the vendor of this provider (e.g. Redis or Cassandra or NATS etc)

`--revision` (Alias `-r`) Monotonically increasing revision number

`--version` (Alias `-e`) Human-friendly version string

`--issuer` (Alias `-i`) Path to issuer seed key (account). If this flag is not provided, the will be sourced from $WASH_KEYS ($HOME/.wash/keys) or generated for you if it cannot be found [env: WASH_ISSUER_KEY]

`--subject` (Alias `-s`) Path to subject seed key (module). If this flag is not provided, the will be sourced from $WASH_KEYS ($HOME/.wash/keys) or generated for you if it cannot be found [env: WASH_SUBJECT_KEY]

`--directory` Location of key files for signing. Defaults to $WASH_KEYS ($HOME/.wash/keys) [env: WASH_KEYS]

`--expires` (Alias `-x`) Indicates the token expires in the given amount of days. If this option is left off, the token will never expire

`--nbf` (Alias `-b`) Not before days. Period in days that must elapse before this token is valid. If this option is left off, the token will be valid immediately

`--disable-keygen` Disables autogeneration of keys if seed(s) are not provided
