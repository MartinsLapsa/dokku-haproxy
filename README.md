# dokku-haproxy

**haproxy tcp load balancer for dokku**

It handles both tcp and http protocols. This is an alternative for [official dokku haproxy plugin](https://dokku.com/docs/networking/proxies/haproxy/) if you need tcp load balancing.

## Installation

Install the plugin:

```bash
dokku plugin:install https://github.com/MartinsLapsa/dokku-haproxy.git
```

### Credits
This plugin is largely inpsired on the HAPRoxy plugin found here:
https://github.com/256dpi/dokku-haproxy

Reason why you could use this plugin over the original HAProxy plugin is that this plugin is integrated with the default proxy management from Dokku.


### Installation Notes
 * This plugin will expose the stats interface on port 9090, its up to you to allow or block this port in your firewall.

## Usage

1. Set app proxy to haproxy.
```bash
dokku proxy:set app_name haproxy
```
2. Set port mappings
```bash
dokku ports:add app_name tcp:host-port:container-port
```

The plugin hooks into the default proxy management of dokku and can work alongside the vhost-nginx plugin for serices that expose TCP ports. Probably the best use cases for this plugin are:
* When an external reverse proxy is used in front of Dokku. Using HAProxy will not impact headers such as forwarder-for etc.
* When using dokku to run (micro)services that expose (multiple) TCP ports
