---
title: "Configure Tyk Enterprise Developer Portal"
date: 2022-02-08
tags: ["Configure Tyk Enterprise Developer Portal", "Tyk Enterprise Developer Portal"]
description: "Configuration reference for the Tyk Enterprise Developer Portal"
menu:
  main:
    parent: "Install Tyk Enterprise Developer Portal"
weight: 1
---


## Tyk Enterprise Developer Portal Configuration Options
To configure the Tyk Enterprise Developer Portal, you can use either a config file or environment variables.
The below table provides reference to all options available to you when configuring the portal.
### Portal settings
This section explains the general portal settings, including which port it will be listening on, how often it should synchronize API Products and plans with the Tyk Dashboard, and so on.
Most of these settings are optional, except for the PORTAL_LICENSEKEY. If you don't specify these settings, the default values will be used.
However, you can leverage the settings below to customize the deployment of your portal.

#### Sample storage setting section via config file
```json
{
  "HostPort": 3001,
  "RefreshInterval": 10,
  "LicenseKey": "your-license-key",
  "Theming": {
    "Theme": "default",
    "Path": "./themes"
  },
  "ProductDocRenderer": "stoplight",
  "LogLevel": "debug",
  "LogFormat": "dev",
  "TLSConfig": {
    "Enable": true,
    "InsecureSkipVerify": true,
    "Certificates": [
      {
        "Name": "localhost",
        "CertFile": "portal.crt",
        "KeyFile": "portal.key"
      }
    ]
  },
  "PortalAPISecret": "your-portal-api-secret"
}
```

#### Sample storage setting section via environment variables
```.ini
PORTAL_HOSTPORT=3001
PORTAL_REFRESHINTERVAL=10
PORTAL_LICENSEKEY=your-license-key
PORTAL_THEMING_THEME=default
PORTAL_THEMING_PATH=./themes
PORTAL_DOCRENDERER=stoplight
PORTAL_LOG_LEVEL=debug
PORTAL_LOG_FORMAT=dev
PORTAL_TLS_ENABLE=true
PORTAL_TLS_INSECURE_SKIP_VERIFY=true
PORTAL_TLS_CERTIFICATES = '[{"Name": "localhost","CertFile": "portal.crt","KeyFile": "portal.key"}]'
PORTAL_API_SECRET=your-portal-api-secret
```

#### PORTAL_HOSTPORT
**Config file:** HostPort <br/>
**Type:** `int` <br/>
**Description**: The port on which the portal will run inside the container. Not required. If it is not specified, the default value is 3001.

#### PORTAL_REFRESHINTERVAL
**Config file:** RefreshInterval <br/>
**Type:** `int` <br/>
**Description**: How the portal will synchronise API Products and plans with the Tyk Dashboard. The value is specified in minutes.
Not required. If it is not specified, the default value is 10.

#### PORTAL_LICENSEKEY
**Config file:** LicenseKey <br/>
**Type:** `string` <br/>
**Description**: A licence key that Tyk provides. Required to start the portal.

#### PORTAL_THEMING_THEME
**Config file:** Theming.Theme <br/>
**Type:** `string` <br/>
**Description**: The name of a theme the portal should use after the start-up. You can change this later via the Themes UI.
It's not required to specify as the portal comes with only one theme named `default`,  therefore, PORTAL_THEMING_THEME defaults `default`.
However, if you already created [a theme]({{< ref "/content/tyk-stack/tyk-developer-portal/enterprise-developer-portal/customise-enterprise-portal/full-customisation/full-customisation.md" >}}) and want the portal to use when it's starts for the first time, then you can use this setting to achieve that.

#### PORTAL_THEMING_PATH
**Config file:** Theming.Path <br/>
**Type:** `string` <br/>
**Description**: Defines a folder where themes are located. Depending on the storage type that you use, you can specify either a relative or an absolute path:
- If you use the `fs` storage type, you can specify both a relative path (e.g., `./themes`) and an absolute path (e.g., `/themes`)
- If you use the `s3` storage type, however, you can only use an absolute path (e.g., `/themes`).

The default value for this variable is `./themes`, so it's important to redefine it if you plan to use the `s3` storage type.

#### PORTAL_DOCRENDERER
**Config file:** ProductDocRenderer <br/>
**Type:** `string` <br/>
**Options:**
- `stoplight` to use Stoplight as a documentation renderer;
- `redoc` to use Redoc as a documentation renderer.

**Description**: Use this setting to specify which OAS documentation renderer to use to render Open API Specification. Not required. If it is not specified, the default value is `stoplight`.

#### PORTAL_LOG_LEVEL
**Config file:** LogLevel <br/>
**Type:** `string` <br/>
**Description**: Defines the log level, available options are:
- debug
- info
- warn
- error
- dpanic
- panic
- fatal

#### PORTAL_LOG_FORMAT
**Config file:** LogFormat <br/>
**Type:** `string` <br/>
**Description**: Defines the log format, available options are:
- `dev` for verbose human-readable output
- `prod` for output in json format.

#### PORTAL_TLS_ENABLE
**Config file:** TLSConfig.Enable <br/>
**Type:** `boolean` <br/>
**Description**: Enables TLS.

#### PORTAL_TLS_INSECURE_SKIP_VERIFY
**Config file:** TLSConfig.InsecureSkipVerify <br/>
**Type:** `boolean` <br/>
**Description**: Skip verification of self-signed certificates.

#### PORTAL_TLS_CERTIFICATES
**Config file:** TLSConfig.Certificates <br/>
**Type:** `json` <br/>
**Description**: JSON (or JSON-formatted string in case of environment variable) containing list of certificates. Each certificate is defined by three properties:
- Name
- CertFile
- KeyFile

#### PORTAL_API_SECRET
**Config file:** PortalAPISecret <br/>
**Type:** `string` <br/>
**Description**: API secret for enabling [Single Sign-on (SSO) flow]({{< ref "/content/tyk-stack/tyk-developer-portal/enterprise-developer-portal/managing-access/enable-sso.md" >}}) with the Tyk Identity Broker.
You can specify any string value in this setting. Omit this setting if you don't require SSO. 

### Storage settings
Using variables from this section, you can configure storage for the portal's CMS assets such as themes, images, and Open API Specification files. The portal supports two types of storage:
- S3 volume;
- And filesystem.

#### Sample storage setting section via config file
```json
{
  "Storage": "s3",
  "S3": {
    "AccessKey": "your-access-key",
    "SecretKey": "your-secret-key",
    "Region": "sa-east-1",
    "Endpoint": "https://s3.sa-east-1.amazonaws.com",
    "Bucket": "your-portal-bucket",
    "ACL": "private",
    "PresignURLs": true
    }
}
```

#### Sample storage setting section via environment variables
```.ini
PORTAL_STORAGE=s3
PORTAL_S3_AWS_ACCESS_KEY_ID=your-access-key
PORTAL_S3_AWS_SECRET_ACCESS_KEY=your-secret-key
PORTAL_S3_REGION=sa-east-1
PORTAL_S3_ENDPOINT=your-portal-bucket
PORTAL_S3_BUCKET=https://s3.sa-east-1.amazonaws.com
PORTAL_S3_ACL=private
PORTAL_S3_PRESIGN_URLS=true
```

#### PORTAL_STORAGE
**Config file:** Storage <br/>
**Type:** `string` <br/>
**Options:**
- `fs` to use file system storage type;
- `s3` to use S3 volume for storing the portal assets.

**Description**: Defines which type of storage to use for the portal's CMS assets. Not required. If it is not specified, the default value is `fs`.

#### PORTAL_S3_AWS_ACCESS_KEY_ID
**Config file:** S3.AccessKey <br/>
**Type:** `string` <br/>
**Description**: Access key for your S3 bucket. This option is only required for the `s3` storage type and will be ignored for the `fs` storage type.

#### PORTAL_S3_AWS_SECRET_ACCESS_KEY
**Config file:** S3.SecretKey <br/>
**Type:** `string` <br/>
**Description**: Secret access key for your S3 bucket. This option is only required for the `s3` storage type and will be ignored for the `fs` storage type.

#### PORTAL_S3_REGION
**Config file:** S3.Region <br/>
**Type:** `string` <br/>
**Description**: AWS region where the S3 bucket is hosted. E.g., `sa-east-1`. This option is only required for the `s3` storage type and will be ignored for the `fs` storage type.

#### PORTAL_S3_ENDPOINT
**Config file:** S3.Endpoint <br/>
**Type:** `string` <br/>
**Description**: URL to object storage service. E.g., `https://s3.sa-east-1.amazonaws.com` or `https://play.min.io`. This option is only required for the `s3` storage type and will be ignored for the `fs` storage type.

#### PORTAL_S3_BUCKET
**Config file:** S3.Bucket <br/>
**Type:** `string` <br/>
**Description**: Name of the S3 bucket. Required only for the `s3` storage type. This option is only required for the `s3` storage type and will be ignored for the `fs` storage type.

#### PORTAL_S3_ACL
**Config file:** S3.ACL <br/>
**Type:** `string` <br/>
**Description**: ACL permissions are set on the bucket, with options including `private`, `public-read`, `public-read-write`, and `authenticated-read`.
If the bucket uses a policy to set permissions, you should leave the ACL value empty. This option is only required for the `s3` storage type and will be ignored for the `fs` storage type.

#### PORTAL_S3_PRESIGN_URLS
**Config file:** S3.PresignURLs <br/>
**Type:** `string` <br/>
**Description**: The PresignURLs option instructs the client to retrieve presigned URLs for the objects.
This is particularly useful if the bucket is private and you need to access the object directly, such as when displaying an image on a web page.
This option is only required for the `s3` storage type and will be ignored for the `fs` storage type.

### Database connection settings
This section provides a reference for the database connection settings used in the portal.
#### Sample database connection setting section via config file
```json
{
  "Database": {
    "Dialect": "mysql",
    "ConnectionString": "admin:secr3t@(localhost:3308)/portal?charset=utf8&parseTime=True&loc=Local",
    "EnableLogs": true,
    "MaxRetries": 3,
    "RetryDelay": 2000
  }
}
```

#### Sample database connection setting section via environment variables
```.ini
PORTAL_DATABASE_DIALECT="mysql"
PORTAL_DATABASE_CONNECTIONSTRING="admin:secr3t@(localhost:3308)/portal?charset=utf8&parseTime=True&loc=Local"
PORTAL_DATABASE_ENABLELOGS=true
PORTAL_DATABASE_MAXRETRIES=3
PORTAL_DATABASE_RETRYDELAY=5000
```

#### PORTAL_DATABASE_DIALECT
**Config file:** Database.Dialect  <br/>
**Type:** `string` <br/>
**Description**: A database will be used to store the portal data. Available dialects are:
- `mysql`
- `postgres`
- `sqlite3`

#### PORTAL_DATABASE_CONNECTIONSTRING
**Config file:** Database.ConnectionString <br/>
**Type:** `string` <br/>
**Description**: Connection string to the selected database. This setting must be present if the `PORTAL_DATABASE_DIALECT` is specified.

#### PORTAL_DATABASE_ENABLELOGS
**Config file:** Database.EnableLogs <br/>
**Type:** `boolean` <br/>
**Description**: Enables logging connection to the database. We recommend disabling this in production environments.

#### PORTAL_DATABASE_MAXRETRIES
**Config file:** Database.MaxRetries <br/>
**Type:** `boolean` <br/>
**Description**: Defines how many times the portal will retry to connect to the database. Optional, the default value is 3.

#### PORTAL_DATABASE_RETRYDELAY
**Config file:** Database.MaxRetries <br/>
**Type:** `boolean` <br/>
**Description**: Defines delay between connect attempts (in milliseconds). Optional, the default value is 5000.


## Sample config file
```json
{
  "HostPort": 3001,
  "RefreshInterval": 10,
  "LicenseKey": "your-license-key",
  "Theming": {
    "Theme": "default",
    "Path": "./themes"
  },
  "ProductDocRenderer": "stoplight",
  "LogLevel": "debug",
  "LogFormat": "dev",
  "TLSConfig": {
    "Enable": true,
    "InsecureSkipVerify": true,
    "Certificates": [
      {
        "Name": "localhost",
        "CertFile": "portal.crt",
        "KeyFile": "portal.key"
      }
    ]
  },
  "PortalAPISecret": "your-portal-api-secret",
  "Storage": "s3",
  "S3": {
    "AccessKey": "your-access-key",
    "SecretKey": "your-secret-key",
    "Region": "sa-east-1",
    "Endpoint": "https://s3.sa-east-1.amazonaws.com",
    "Bucket": "your-portal-bucket",
    "ACL": "private",
    "PresignURLs": true
  },
  "Database": {
    "Dialect": "mysql",
    "ConnectionString": "admin:secr3t@(localhost:3308)/portal?charset=utf8&parseTime=True&loc=Local",
    "EnableLogs": true,
    "MaxRetries": 3,
    "RetryDelay": 2000
  }
}
```
## Sample .env file
```ini
PORTAL_HOSTPORT=3001
PORTAL_REFRESHINTERVAL=10
PORTAL_LICENSEKEY=your-license-key
PORTAL_THEMING_THEME=default
PORTAL_THEMING_PATH=./themes
PORTAL_DOCRENDERER=stoplight
PORTAL_LOG_LEVEL=debug
PORTAL_LOG_FORMAT=dev
PORTAL_TLS_ENABLE=true
PORTAL_TLS_INSECURE_SKIP_VERIFY=true
PORTAL_TLS_CERTIFICATES = '[{"Name": "localhost","CertFile": "portal.crt","KeyFile": "portal.key"}]'
PORTAL_API_SECRET=your-portal-api-secret
PORTAL_STORAGE=s3
PORTAL_S3_AWS_ACCESS_KEY_ID=your-access-key
PORTAL_S3_AWS_SECRET_ACCESS_KEY=your-secret-key
PORTAL_S3_REGION=sa-east-1
PORTAL_S3_ENDPOINT=your-portal-bucket
PORTAL_S3_BUCKET=https://s3.sa-east-1.amazonaws.com
PORTAL_S3_ACL=private
PORTAL_S3_PRESIGN_URLS=true
PORTAL_DATABASE_DIALECT="mysql"
PORTAL_DATABASE_CONNECTIONSTRING="admin:secr3t@(localhost:3308)/portal?charset=utf8&parseTime=True&loc=Local"
PORTAL_DATABASE_ENABLELOGS=true
PORTAL_DATABASE_MAXRETRIES=3
PORTAL_DATABASE_RETRYDELAY=5000
```
