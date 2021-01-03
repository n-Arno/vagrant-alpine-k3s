vagrant-alpine-k3
=================

K3S installation procedure got very simple even on Alpine:

```
curl -sfL https://get.k3s.io | sh -
  # Check for Ready node, 
  takes maybe 30 seconds
  k3s kubectl get node
```

This repo is now archived for history only.

-----------------

Quick and dirty vagrant file to start K3S in an alpine.

Check [K3S repository](https://github.com/rancher/k3s) for more on this project

NB: `kubectl` is set up as an alias of `sudo k3s kubectl`
