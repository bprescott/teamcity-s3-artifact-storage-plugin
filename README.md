[![official project](http://jb.gg/badges/official.svg)](https://confluence.jetbrains.com/display/ALL/JetBrains+on+GitHub) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) <a href="https://teamcity.jetbrains.com/viewType.html?buildTypeId=TeamCityPluginsByJetBrains_AwsS3ArtifactStorage_TeamCityTrunk&tab=buildTypeHistoryList&guest=1"><img src="https://teamcity.jetbrains.com/app/rest/builds/buildType:(id:TeamCityPluginsByJetBrains_AwsS3ArtifactStorage_TeamCityTrunk)/statusIcon.svg" alt=""/></a>

# TeamCity S3 Artifact Storage Plugin

This plugin allows replacing the TeamCity built-in artifacts storage with [AWS S3](https://aws.amazon.com/s3/). The artifacts storage can be changed at the project level. After changing the storage, new artifacts produced by the builds of this project will be published to the (specified) AWS S3 bucket. Besides publishing, the plugin also implements resolving of artifact dependencies and clean-up of build artifacts.

# State

Baseline functionality finished. Feedback wanted.

# Compatibility

The plugin is compatible with [TeamCity](https://www.jetbrains.com/teamcity/download/) 2017.1 and greater

# Features

When installed and configured, the plugin:
* allows uploading artifacts to Amazon S3
* allows downloading and removing artifacts from Amazon S3
* handles resolution of artifact dependencies
* handles clean-up of artifacts 
* displays artifacts located in Amazon S3 in the TeamCity web UI.
* creates a custom s3 tree structure to support unpublished,published, released etc.

# Building 

Issue the `mvn package` command from the root project to build your plugin. The resulting \<artifactId>.zip package will be placed in the 'target' directory. 

# Download

| Download | Compatibility |
|----------|---------------|
|[Download](https://plugins.jetbrains.com/plugin/9623-s3-artifact-storage)| 2017.1.1 |


# Installing

See [instructions](https://confluence.jetbrains.com/display/TCDL/Installing+Additional+Plugins) in TeamCity documentation.

# Configuring 

The plugin adds the Artifacts Storage tab to the Project Settings page in the TeamCity Web UI. 
The tab lists the built-in TeamCity artifacts storage displayed by default and marked as active.

To configure Amazon S3 storage for TeamCity artifacts, perform the following:
1. Select S3 Storage as the storage type.
2. Provide an optional name for your storage.
3. Select an AWS region.
4. Provide your AWS Security Credentials.
5. Specify an existing S3 bucket to store artifacts.
6. Save your settings.
7. The configured S3 storage will appear on the Artifacts storage page. Make it active using the corresponding link.
8. To setup the deployment path names in s3 you need to set a few parameters
   version - the version of the artifact
   build_target - this is the target directory for the build
   deploy_type - this is the type of deployment (unpublished, published, released, experimental...)
   The constructed path is target_deploy/project/version/build_target

Now the artifacts of this project, its subprojects, and build configurations will be stored in the configured storage.


