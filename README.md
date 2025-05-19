# Automatic Ser2Net

This is a small tool that generates a config for [ser2net](https://github.com/cminyard/ser2net) based on discovered USB serial devices.

It replaces the stock entrypoint script with one that introspects the Linux `/sys` tree to generate a set of configs that match the hardware you have.

To add a new device type, create a file named `scripts/<vendor_id>:<product_id>.yaml` with your desired `ser2net` connection YAML, using the literal string `DEVNODE` in place of an explicit device path.

## Default Port Assignments

6636 - generator (rs232 interface)
6637 - waterfurnace (rs485 interface)
6638 - zwave
6639 - zigbee

## Deploying

See the example Kubernetes manifest in `manifests/app.yaml`.
Note that if you are deploying into a Kubernetes cluster with Pod Security Admission you'll need to add these annotations to the namespace where you deploy ser2net-auto:

```
pod-security.kubernetes.io/audit=privileged
pod-security.kubernetes.io/enforce=privileged
pod-security.kubernetes.io/warn=privileged
```

## Licence

The software in this repo is copyright (C) Pete Keen and licensed with the MIT license.

The resulting image bundles software that is copyright (C) Corey Minyard <minyard@acm.org> and licensed with GPL 2.0.
