---
title: "Datadog"
date: 2021-08-02T20:22:57-10:00
---

Using Datadog is _hard_. Personally, I've been using Datadog for at
least six or seven years (as of 2021). It's the telemetry tool I'm
most familiar with. This guide collects some snippets and useful
things I've learned over the years. At a mimimum this is a resource
that I can revist when I need to remember how I did that _one_ thing
all that time ago. Oh, did I forget that their docs are so-so and the
product has a weird UX bugs? Perhaps this guide can smooth some of
those rough patches.

## Nginx Ingress Controller Integration

_Last Encountered: August 2021_

The [nginx ingress integration][nginx ingress] docs are not clear
exactly what to do. They assume you already understand Kubernetes
autodiscovery (i.e. configuration Datadog integrations by adding
annotations to k8s resources) and you know how to get values into
Kubernetes objects. This is not immediately obvious if you're using
the official Nginx Ingress Helm chart. Luckily the chart has the
appropriate values to make it works.

Here's a sample `values.yaml` file you can use in combination with the
chart to setup:

1. Ingress controller metrics (for USE metrics)
2. Nginx status check (for uptime monitoring)
3. Log parsing (so logs make sense out of the box)
4. Overall http check (for uptime monitoring)

These values are tested against Helm chart `3.34.0` release in July 2021.

```yaml
controller:
  podLabels:
    tags.datadoghq.com/env: prod
    tags.datadoghq.com/service: my-ingress
  podAnnotations:
    ad.datadoghq.com/controller.check_names: |
      [ "nginx", "nginx_ingress_controller" ]
    ad.datadoghq.com/controller.init_configs: |
      [{ }, { }]
    ad.datadoghq.com/controller.instances: |
      [
        {
          "nginx_status_url": "http://%%host%%:18080/nginx_status"
        }, {
          "prometheus_url": "http://%%host%%:10254/metrics"
        }
      ]
    ad.datadoghq.com/controller.logs: |
      [{ "source": "nginx-ingress-controller" }]
  service:
    labels:
      tags.datadoghq.com/env: prod
      tags.datadoghq.com/service: my-ingress
    annotations:
      ad.datadoghq.com/service.check_names: |
        [ "http_check" ]
      ad.datadoghq.com/service.init_configs: |
        [{ }]
      ad.datadoghq.com/service.instances: |
        [{
          "name": "ingress-tools-v2",
          "url": "http://%%host%%/healthz"
        }]
  metrics:
    enabled: true
  config:
    http-snippet: |
      server {
        listen 18080;

        location /nginx_status {
          allow all;
          stub_status on;
        }

        location / {
          return 404;
        }
      }
```

[use metrics]: https://www.brendangregg.com/usemethod.html
[nginx ingress]: https://docs.datadoghq.com/integrations/nginx_ingress_controller/
