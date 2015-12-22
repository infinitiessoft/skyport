# skyport

Skyport is an open source Java application that enables user to use [Openstack Nova 2.0 API](http://developer.openstack.org/api-ref-compute-v2.html) to manage multicloud environment.

#Table of contents

- [Overview](#overview)
- [Installation](#installation)
- [Configuration](#configuration)
    - [Profile](#profile)
    - [Security](#security)
        - [Disabling Authentication](#disabling-authentication)
        - [Integrate with `Openstack Keystone` or `Keystone4j`](#integration-with-openstack-keystone_or_keystone4j)
            - [Configure `policy.json`](#configure-policy.json)
- [Using Rest API](#using-rest-api)
- [Release notes](#release-notes)
- [Acknowledgements](#acknowledgements)
- [License](#license)

## Overview

For some reason, many of us use multiple virtualization platform concurrently. But the more platforms you use, the more work it takes to keep up with them. Skyport is an application that provides a single API compatibility with [Openstack Nova 2.0 API](http://developer.openstack.org/api-ref-compute-v2.html) to work with multiple cloud computing providers.

## Installation

The lastest binary downloads of the Skyport4 are available [here] (https://github.com/infinitiessoft/skyport/releases/download/v4.0.0-alpha/skyport4.0.0-SNAPSHOT-20151219-1120.zip). Unpack the binary distribution so that it resides in its own directory (conventionally named "skyport[version]"). Skyport can be run as a service using the `skyport` script located under bin/ location. The script accepts a single parameter with the following values:

    console: Run Skyport in the foreground.

    start: Run Skyport in the background.

    stop: Stops Skyport if its running.

    install: Install Skyport to run on system startup (windows only).

    remove: Removes Skyport from system startup (windows only).

Skyport uses Java Service Wrapper which is a small native wrapper around the Java virtual machine which also monitors it. Note, passing JVM level configuration (such as -X parameters) should be set within the conf/wrapper.conf file.The wrapper.java.maxmemory environment variable controls the maximum memory allocation for the JVM (set in megabytes). It defaults to 512. For more information about configuring Java Service Wrapper, refer to [Java Service Wrapper](http://wrapper.tanukisoftware.com/doc/english/properties.html)

## Configuration

### Profile

To add or configure a Profile on Skyport, use the Skyport Administrator GUI.

  1. To create a Profile, click the **Add** button.
  2. You now need to configure the specific fields for the Cloud Services Profile you are creating through the Configuration dialog.
   ![Alt text](https://github.com/infinitiessoft/skyport/blob/master/image/configuration_dialog.png "Configuration Dialog")
    * `Id`:Enter the identifier of the profile to access **(Optional)**. If Id field is left blank the Profile is assigned an automatically generated Id by Skyport.
    * `Name`:Enter some text to help identify the profile **(Required)**. It can be any valid name that you choose.
    * `Provider Class`:Select the Cloud Services driver for this profile **(Required)**.
    * `Provider`:Select the Cloud Service Provider you want to connect to **(Required)**.
    * `Endpoint`:Enter the URL at which the Cloud Services API is sitting **(Required)**.
    * `Account`:Enter the account/tenant Id to which your API keys are tied **(Required)**.
    * `RegionId`:Enter the id for the region you are working against **(Required)**.
    * `AccessPublic`:Enter the public part of your API keys or username **(Required)**.
    * `AccessPrivate`:Enter the private part of your API keys or password **(Required)**.

  3. To enable cache to reduce the response time of the API, select the **Cache** check box to enable caching.
  4. To enable timeout mechanism of the API , select the **Timeout** check box to enable Timeout mechanism. 
  5. To verify the profile using the parameter you have entered, click the **Test** button. If the connection could be made successfully, you will be notified with a *Connection Successfully!* dialog.
  6. You can configure a number of options for a specific Profile by using the **Advance** button.
  ![Alt text](https://github.com/infinitiessoft/skyport/blob/master/image/advance_dialog.png "Advance Dialog")
  Each profile holds three threadpools for segregating application resources between different types of task - short-term, medium-term and long-term. You can configure those threadpools in the top of the Advance dialog:

   * `Core size`:The number of threads to keep in the pool, even if they are idle.
   * `Max size`:The maximum number of threads to allow in the pool.
   * `Queue capacity`:The maximum work queue size of the thread pool.

   By clicking on the function name within the tree view in the left-side panel, the right side of the Advance dialog will load the function settings and allows you to modify these setting.
   
   * `ThreadPool`:The threadPool on which the function is assigned to.
   * `Delay`:A fixed period between the end of the last invocation and the start of the next(Caching only).
   * `Timeout`:The maximum time to wait for function execution completely(Timeout only).

  7. Click **OK** to save the Profile.

### Security

#### Disabling Authentication

Skyport normally enforce *noauth* authentication strategy.
This is configured in the *config/nova.conf* file:

```config/nova.conf
# The strategy to use for auth: noauth or keystone. (string
# value)
auth_strategy=noauth
```

The *noauth* strategy still performs authentication, but does not validate any credentials. It provides administrative credentials only if 'admin' is specified as the username.
With this strategy registered, any access to the server with token format like ``X-Auth-Token:{profile_id}:admin`` will be granted for admin privilege.

#### Integrate with `Openstack Keystone` or `Keystone4j`



##### Configure `policy.json`

## Using Rest API
Skyport default listens on port 9999. The examples in this section use [cURL](http://curl.haxx.se/) commands. For information about the OpenStack Compute(Nova) 2.0 APIs, see [Openstack Nova 2.0 API Reference](http://developer.openstack.org/api-ref-compute-v2.html). Using a cURL command like the following command to list servers:

```curl
curl -H "X-Auth-Token:{token}" http://localhost:9999/v2/{profile_id}/servers
```

example response:

```json
{
  "servers" : [ {
    "id" : "f2f5ca29-6c6d-4241-ab05-cc631da2486e",
    "name" : "3TLTCrryMQiM",
    "links" : [ {
      "rel" : "self",
      "href" : "http://localhost:9999/v2/98f4cd52-fa8b-4e5f-a031-bc73686cf3fc/servers/f2f5ca29-6c6d-4241-ab05-cc631da2486e"
    }, {
      "rel" : "bookmark",
      "href" : "http://localhost:9999/98f4cd52-fa8b-4e5f-a031-bc73686cf3fc/servers/f2f5ca29-6c6d-4241-ab05-cc631da2486e"
    } ]
  }, {
    "id" : "8d8679af-f2fd-42b3-9803-1a294b75f91a",
    "name" : "cirros",
    "links" : [ {
      "rel" : "self",
      "href" : "http://localhost:9999/v2/98f4cd52-fa8b-4e5f-a031-bc73686cf3fc/servers/8d8679af-f2fd-42b3-9803-1a294b75f91a"
    }, {
      "rel" : "bookmark",
      "href" : "http://localhost:9999/98f4cd52-fa8b-4e5f-a031-bc73686cf3fc/servers/8d8679af-f2fd-42b3-9803-1a294b75f91a"
    } ]
  }, {
    "id" : "127dbebd-d189-4124-8bd3-4a35dc638909",
    "name" : "cirrow-jcnet",
    "links" : [ {
      "rel" : "self",
      "href" : "http://localhost:9999/v2/98f4cd52-fa8b-4e5f-a031-bc73686cf3fc/servers/127dbebd-d189-4124-8bd3-4a35dc638909"
    }, {
      "rel" : "bookmark",
      "href" : "http://localhost:9999/98f4cd52-fa8b-4e5f-a031-bc73686cf3fc/servers/127dbebd-d189-4124-8bd3-4a35dc638909"
    } ]
  }, {
    "id" : "30d563ce-f7a7-476a-b7e9-9baa1b2a4453",
    "name" : "cirros",
    "links" : [ {
      "rel" : "self",
      "href" : "http://localhost:9999/v2/98f4cd52-fa8b-4e5f-a031-bc73686cf3fc/servers/30d563ce-f7a7-476a-b7e9-9baa1b2a4453"
    }, {
      "rel" : "bookmark",
      "href" : "http://localhost:9999/98f4cd52-fa8b-4e5f-a031-bc73686cf3fc/servers/30d563ce-f7a7-476a-b7e9-9baa1b2a4453"
    } ]
  } ]
}
```

## Dependencies

Java Runtime Environment 1.7 or above is required to run Skyport.

## Release notes

Check them here: [Release notes](https://github.com/infinitiessoft/skyport/blob/master/RELEASENOTES.md)

## Acknowledgements

The Skyport infrastructure relies upon these free and openly available projects:
- [OpenStack compute(Nova)](https://github.com/openstack/nova)
- [Dasein clouds](https://github.com/dasein-cloud/dasein-cloud/)
- [Java Websockify](https://github.com/jribble/Java-Websockify)

## License

*Skyport* is available under the Apache License, Version 2.0.

(c) All rights reserved InfinitiesSoft Solutions Inc.
