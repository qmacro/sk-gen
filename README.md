# Service key generator

Makes temporary (limited lifetime) service keys available:

Uses `generate` to:

- determine the name of the service key (`<sk_prefix>-<timestamp>`)
- create a service key with that name for the service instance
- retrieves the JSON value of the service key's `credentials` property
- stores the JSON in a password-protected ZIP file, in the `keys/` dir

Uses `cleanup` to:

- look through files in the `keys/` dir
- identify those, via the timestamp suffix in their names, that should be expired due to their age
- deletes the service key and the file, for those identified

Need to define values for the following - use GitHub repo secrets / env vars in workflows:

|Type|Name|Default|Purpose|
|-|-|-|-|
|Var|SK_PREFIX|`sk`|Service key name prefix (a timestamp suffix will be appended to this)|
|Var|SK_MAX_AGE|30|How long a service key should live (mins)|
|Var|CF_SERVICE_INSTANCE|-|Name of the service instance for which keys should be created|
|Secret|SK_PASSWORD|-|Password to protect ZIP file|
|Secret|CF_API|-|The API endpoint for CF auth|
|Secret|CF_USERNAME|-|The name of the user for CF auth|
|Secret|CF_PASSWORD|-|The password for CF auth|
|Secret|CF_ORG|-|The CF org to target|
|Secret|CF_SPACE|-|The CF space to target|

Users of such keys should always be instructed to *take the **latest** service key file in the `keys/` dir*.
