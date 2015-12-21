# skyport

Skyport is an open source Java application that enables user to use [Openstack Nova 2.0 API](http://developer.openstack.org/api-ref-compute-v2.html) to manage multicloud environment.

#Table of contents

- [Quick start](#quick-start)
- [Overview](#overview)
- [Configuration](#configuration)
    - [Profile](#profile)
    - [Security](#security)
        - [Disabling Authentication](#disabling-authentication)
        - [Integrate with `Openstack Keystone`](#integration-with-openstack-keystone)
        - [Integrate with `Keystone4j`](#_integration-with-keystone4j)
        - [Configure `policy.json`](# configure-policy.json)
- [Release notes](#release-notes)
- [Acknowledgements](#acknowledgements)
- [License](#license)

## Quick start

The lastest binary downloads of the Skyport4 are available [here] (https://github.com/infinitiessoft/skyport/releases/download/v4.0.0-alpha/skyport4.0.0-SNAPSHOT-20151219-1120.zip). Unpack the binary distribution so that it resides in its own directory (conventionally named "skyport[version]"). Skyport can be run as a service using the `skyport` script located under bin/ location. The script accepts a single parameter with the following values:

    console: Run Skyport in the foreground.

    start: Run Skyport in the background.

    stop: Stops Skyport if its running.

    install: Install Skyport to run on system startup (windows only).

    remove: Removes Skyport from system startup (windows only).

Skyport uses Java Service Wrapper which is a small native wrapper around the Java virtual machine which also monitors it. Note, passing JVM level configuration (such as -X parameters) should be set within the conf/wrapper.conf file.The wrapper.java.maxmemory environment variable controls the maximum memory allocation for the JVM (set in megabytes). It defaults to 512. For more information about configuring Java Service Wrapper, refer to [Java Service Wrapper](http://wrapper.tanukisoftware.com/doc/english/properties.html)

## Overview

For some reason, many of us use multiple virtualization platform concurrently. But the more platforms you use, the more work it takes to keep up with them. Skyport is an application that provides a single API compatibility with [Openstack Nova 2.0 API](http://developer.openstack.org/api-ref-compute-v2.html) to work with multiple cloud computing providers.

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

  3. To enable cache to reduce the response time of the List Objects API, select the **Cache** check box to enable caching.
  4. To enable timeout mechanism of the API , select the **Timeout** check box to enable Timeout mechanism. 
  5. To verify the profile using the parameter you have entered, click the **Test** button. If the connection could be made successfully, you will be notified with a *Connection Successfully!* dialog.
  6. You can configure a number of options for a specific Profile by using the **Advance** button.
  ![Alt text](https://github.com/infinitiessoft/skyport/blob/master/image/advance_dialog.png "Advance Dialog")
  7. Click **OK** to save the Profile.

### Security

#### Disabling Authentication

#### Integrate with `Openstack Keystone`

#### Integrate with `Keystone4j`

#### Configure `policy.json`

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
