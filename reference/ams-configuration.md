<!-- DO NOT EDIT THIS FILE. IT IS GENERATED AUTOMATICALLY. -->
<!-- Edit ams-configuration.tmpl.md and ams-configuration.yaml instead. -->

AMS provides various configuration items to customise its behaviour. The following table lists the available configuration items and their meaning.

| Name | Type | Default |  Description            |
|------|------|---------|-------------------------|
| `application.addons` | string | - | Comma-separated list of addons that every application managed by AMS will use. See [How to enable an addon globally](https://discourse.ubuntu.com/t/enable-an-addon-globally/25285). |
| `application.auto_publish` | bool | true | If set to `true`, AMS automatically published new application versions when the bootstrap process is finished. `false` disables this. See [Publish application versions](https://discourse.ubuntu.com/t/update-an-application/24201#publish-application-versions-1). |
| `application.auto_update` | bool | true | If set to `true`, AMS automatically updates applications whenever any dependencies (parent image, addons, global configuration) change. `false` disables this. See [Configure automatic application updates](https://discourse.ubuntu.com/t/update-an-application/24201#configure-automatic-application-updates-3). |
| `application.default_abi` | string | - | Default Android ABI that applications should use. See [Android ABIs](https://developer.android.com/ndk/guides/abis) for a list of available ABIs. |
| `application.max_published_versions` | integer | 3 | Maximum number of published versions per application. If the number of versions of an application exceeds this configuration, AMS will automatically clean up older versions. |
| `container.apt_mirror` | string | - | APT mirror to use within the containers. By default, `http://archive.ubuntu.com` (amd64) or `http://ports.ubuntu.com` (arm64) is used. This configuration item is deprecated since 1.20, use `instance.apt_mirror` instead. |
| `container.default_platform` | string | - | The name of the platform that Anbox Cloud uses by default to launch containers. This configuration item is deprecated since 1.20, use `instance.default_platform` instead. |
| `container.features` | string | - | Comma-separated list of features to enable (see list below). This configuration item is deprecated since 1.20, use `instance.features` instead. |
| `container.network_proxy` | string | - | Network proxy to use inside the containers. This configuration item is deprecated since 1.20, use `instance.network_proxy` instead. |
| `container.security_updates` | bool | true | If set to `true`, automatic Ubuntu security updates are applied during the application bootstrap process. `false` disables this. |
| `core.proxy_http` | string | - | HTTP proxy to use for HTTP requests that AMS performs. |
| `core.proxy_https` | string | - | HTTPS proxy to use for HTTPS requests that AMS performs. |
| `core.proxy_ignore_hosts` | string | - | Comma-separated list that defines the hosts for which a configured proxy is not used. |
| `core.trust_password` | string | - | The AMS trust password. |
| `cpu.limit_mode` | string | scheduler | The mode AMS uses to limit CPU access for an instance. See [About performance](https://discourse.ubuntu.com/t/about-performance/29416) for details. Possible values are: `scheduler`, `pinning` |
| `gpu.allocation_mode` | string | `all` | Method of allocating GPUs: `all` tells AMS to allocate all available GPUs on a system to an instance. `single` allocates only a single GPU. |
| `gpu.type` | string | `none` | Type of GPU: `none`, `intel`, `nvidia`, `amd` |
| `images.allow_insecure` | bool | false | If set to `true`, AMS allows accepting untrusted certificates provided by the configured image server. |
| `images.auth` | string | - | Authentication details for AMS to access the image server. When reading this configuration, a Boolean value that indicates whether the item is set is returned, to avoid exposing credentials. |
| `images.update_interval` | string | `5m` | Frequency of image updates (for example: 1h, 30m). |
| `images.url` | string | `https://images.anbox-cloud.io/stable/` | URL of the image server to use. |
| `images.version_lockstep` | bool | true | Whether to put the version of the latest pulled image and the AMS version in a lockstep. This ensures that a deployment is not automatically updated to newer image versions if AMS is still at an older version. This only applies for new major and minor but not patch version updates. |
| `instance.apt_mirror` | string | - | APT mirror to use within the instances. By default, `http://archive.ubuntu.com` (amd64) or `http://ports.ubuntu.com` (arm64) is used. |
| `instance.default_platform` | string | - | The name of the platform that Anbox Cloud uses by default to launch instances. |
| `instance.features` | string | - | Comma-separated list of features to enable (see list below). |
| `instance.network_proxy` | string | - | Network proxy to use inside the instances. |
| `instance.security_updates` | bool | true | If set to `true`, automatic Ubuntu security updates are applied during the application bootstrap process. `false` disables this. This configuration item is deprecated since 1.20, use `instance.security_updates` instead. |
| `load_balancer.url` | string | - | URL of the load balancer behind which AMS sits. The URL is handed to instances started by AMS to allow them to contact AMS through the load balancer and not via the address of an individual AMS instance. |
| `node.queue_size` | integer | 100 | Maximum size of the queue containing requests to start and stop instances per LXD node. Changing the value requires a restart of AMS. |
| `node.workers_per_queue` | integer | 4 | Number of workers processing instance start and stop requests. Changing the value requires a restart of AMS. |
| `registry.filter` | string | - | Comma-separated list of tags to filter for when applications are fetched from the [Anbox Application Registry](https://discourse.ubuntu.com/t/application-registry/17761). If empty, no filter is applied. |
| `registry.fingerprint` | string | - | Fingerprint of the certificate that the [Anbox Application Registry](https://discourse.ubuntu.com/t/application-registry/17761) uses to TLS-secure its HTTPS endpoint. This is used by AMS for mutual TLS authentication with the registry. |
| `registry.mode` | string | `pull` | Mode in which the [Anbox Application Registry](https://discourse.ubuntu.com/t/application-registry/17761) client in AMS operates: `manual`, `pull`, `push` |
| `registry.update_interval` | string | `1h` | Frequency of [Anbox Application Registry](https://discourse.ubuntu.com/t/application-registry/17761) updates (for example: 1h, 30m). |
| `registry.url` | string | - | URL of the [Anbox Application Registry](https://discourse.ubuntu.com/t/application-registry/17761) to use. |
| `scheduler.strategy` | string | `spread` | Strategy that the internal instance scheduler in AMS uses to distribute instances across available LXD nodes: `binpack`, `spread` |

## Node-specific configuration

In a cluster setup, there are configuration items that can be customised for each node. The following table lists the available configuration items and their meaning.

| Name | Type | Default |  Description            |
|------|------|---------|-------------------------|
| `cpu-allocation-rate` | integer | 4 | CPU allocation rate used for [over-committing resources](https://discourse.ubuntu.com/t/about-capacity-planning/28717#over-committing-resources-3). |
| `cpus` | integer | all available | Number of CPUs dedicated to instances. |
| `gpu-encoder-slots` | integer | 0 (for nodes without GPU or with AMD GPU)<br/>32 (for nodes with NVIDIA GPU)<br/>10 (for nodes with Intel GPU) | Number of GPU encoder slots available on the node. |
| `gpu-slots` | integer | 0 (for nodes without GPU)<br/>32 (for nodes with NVIDIA GPU)<br/>10 (for nodes with AMD or Intel GPU) | Number of [GPU slots](https://discourse.ubuntu.com/t/about-capacity-planning/28717#gpu-slots-2) available on the node. |
| `memory` | integer | all available | Memory dedicated to instances. |
| `memory-allocation-rate` | integer | 2 | Memory allocation rate used for [over-committing resources](https://discourse.ubuntu.com/t/about-capacity-planning/28717#over-committing-resources-3). |
| `public-address` | string | - | The public, reachable address of the node. |
| `subnet` | string | - | The network subnet of the machine where the node runs. |
| `tags` | string | - | Tags to identify the node. |
| `unschedulable` | bool | false | If set to `true`, the node cannot be scheduled, which prevents new instances from being launched on it. |

See [Configure cluster nodes](https://discourse.ubuntu.com/t/configure-cluster-nodes/28716) for instructions on how to set these configuration items.

## Features

Anbox Cloud includes some features which are not enabled by default but can be conditionally enabled. The features are enabled by flags which are configured through AMS. You can configure the feature flags either globally for all instances or per application.

To configure a feature globally for all instances, use a command similar to the following:

    amc config set instance.feature foo,bar

To configure a feature for one application in the manifest, use a syntax similar to the following:

    name: my-app
    instance-type: a4.3
    features: ["foo", "bar"]

#### System UI

By default, Anbox hides the Android system UI when an application is running in foreground mode. In some use cases, however, it's required to have the system UI available for navigation purposes. This can be enabled with the `enable_system_ui` feature flag.

The feature flag will be considered by all new launched instances once set.

#### Virtual Keyboard

The Android virtual keyboard is disabled by default but can be enabled with the `enable_virtual_keyboard` feature flag.

For the feature to be considered, applications must be manually updated, because changes to allow the feature to work are only applied during the [application bootstrap process](https://discourse.ubuntu.com/t/managing-applications/17760#bootstrap-process-2).

#### Client-Side Virtual Keyboard

The client-side virtual keyboard is disabled by default but can be enabled with the `enable_anbox_ime` feature flag. It requires the client application to embed [Anbox WebView](https://discourse.ubuntu.com/t/integrate-a-client-side-virtual-keyboard/23643) which interacts with the client-side virtual keyboard for text editing and sends the text to the Android container.

For the feature to be considered, applications must be manually updated, because changes to allow the feature to work are only applied during the [application bootstrap process](https://discourse.ubuntu.com/t/managing-applications/17760#bootstrap-process-2).

#### WiFi

By default, Anbox sets up a virtual WiFi device, which sits on top of an Ethernet connection and simulates a real WiFi connection. This WiFi support can be optionally disabled with the `disable_wifi` feature flag.

The feature flag will be considered by all newly launched instances once set.

#### Android reboot

By default, Android is not allowed to reboot. With the `allow_android_reboot` feature flag, this can be allowed.

Note that you must disable the [watchdog](https://discourse.ubuntu.com/t/application-manifest/24197#watchdog-5) if reboots are allowed.

The feature flag will be considered by all newly launched instances once set.

#### AV1 software encoder

*since 1.17.0*

The AV1 software encoder is disabled by default but can be enabled with the `experimental.force_av1_software_encoding` feature flag. To transcode the video stream encoded in AV1 codec, all clients must support AV1 decoding.

Once set, this feature flag will be considered by all newly launched instances.

#### Development settings

*since 1.18.0*

The Android development settings (which include an ADB connection) are enabled by default. Some applications require these settings to be disabled, which you can do with the `disable_development_settings` feature flag.

Once set, this feature flag will be considered by all newly launched instances.

#### Custom Android ID

*since 1.18.0*

To enable the Android container to use a custom Android ID, add the feature flag `android.allow_custom_android_id` upon application creation. A system app can influence the Android ID of a specific app during the Android runtime by setting the system property in the format of:
  ```
  `anbox.custom_android_id.<index>=<package_name>:<android_id>`
  ```

 * The `<index>` is a number in the range from 0 to 126, which allows you to have multiple overrides for different packages. If the same `<package_name>` with the different `<android_id>` is given for multiple system properties `anbox.custom_android_id.<index>`, the Android ID read from the system property which has the highest suffixing index that will be used in the end.
 * The `<package_name>` is the package name of the application.
 * The `<android_id>` is a unique ID that represents the Android ID for the targeting application. It must be at least 16 characters in length.

Once set, this feature flag will be considered by all newly launched instances.

#### GL Async Swap Support

*since 1.19.0*

GL Async swap support is enabled by default for explicit signals of buffer swaps completion. To disable the GL async object feature, add the feature flag `emugl.disable_async_swap_support` upon application creation. Once the async swap support is disabled, Anbox Cloud will not use the host GL driver fence commands and file descriptors to synchronise the finished frames between the host and guest. Instead, it will fully rely on the host GPU driver to do so. The environment variable `ANBOX_ASYNC_SWAP_DISABLED_PACKAGES` that accepts a comma-separated list of package names can be used to prevent certain packages from using the async object.

Once set, this feature flag will be considered by all newly launched instances.

#### WebRTC ICE candidate logging

*since 1.20.2*

For debugging purposes, Anbox Cloud can log ICE candidates from the server and client inside the system log of an instance. This is disabled by default and needs to be explicitly turned on with the feature flag `webrtc.enable_ice_logging`.

Once set, this feature flag will be considered by all newly launched instances.
