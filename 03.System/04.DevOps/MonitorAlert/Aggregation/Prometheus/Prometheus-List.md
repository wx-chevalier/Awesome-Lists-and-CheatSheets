# Prometheus List

# OpenSource

- [Prometheus ![code](https://ng-tech.icu/assets/code.svg)](https://prometheus.io/): Prometheus, a Cloud Native Computing Foundation project, is a systems and service monitoring system. It collects metrics from configured targets at given intervals, evaluates rule expressions, displays the results, and can trigger alerts if some condition is observed to be true.

- [Thanos ![code](https://ng-tech.icu/assets/code.svg)](https://thanos.io/): Open source, highly available Prometheus setup with long term storage capabilities.

- [2020-Kvass ![code](https://ng-tech.icu/assets/code.svg)](https://cubox.pro/c/v794lW): Kvass 是一个 Prometheus 横向扩缩容解决方案，他使用 Sidecar 动态得根据 Coordinator 分配下来的 target 列表来为每个 Prometheus 生成只含特定 target 的配置文件，从而将采集任务动态调度到各个 Prometheus 分片。Coordinator 用于服务发现，target 调度和分片扩缩容管理. Thanos (或者其他 TSDB) 用来将分片数据汇总成全局数据.
