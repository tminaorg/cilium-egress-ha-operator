## Description

It is simple k8s operator based on [Flant shell-operator](https://github.com/flant/shell-operator) for egress HA-mode of Cilium.

[Cilium](https://cilium.io/) has an amazing feature called [egress](https://docs.cilium.io/en/stable/network/egress-gateway/), that allows you to redirect outbound traffic form specific pods to specific nodes(via labels). This is a very common case, for example, if you need to send a WhiteList IPs to your third partners. 

Unfortunately, [community version of Cilium doesn't have HA-mode for egress](https://github.com/cilium/cilium/issues/18230).

This operator implements a simple HA-mode for egress. It is assumed that you have 2 "empty" with low resources(for example, 2/2) nodes for egress (similar to ingress). Let's say that by default the node for egress traffic is called egress-1. If this node goes into state "Not Ready", this operator will override all manifests for egress and replace this node there with reserve egress-2. 

This process takes about 30s.

## Deployment

- build image & push to your registry

- edit manifests in `operator.yaml`

- `kubectl -n <namespace> apply -f operator.yaml`

  
