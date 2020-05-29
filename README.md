**创建gitlab runner**

`helm repo add gitlab https://charts.gitlab.io/`
`helm install --namespace gitlab gitlab-runner -f values.yaml gitlab/gitlab-runner`

**gitlab runner创建后需要添加下面内容到/home/gitlab-runner/.gitlab-runner/config.toml**

```
[[runners.kubernetes.volumes.pvc]]
  name = "gitlab-runner-cache-pvc" # 阿里云上创建的pvc名字
  mount_path = "/opt/cache"
  readonly = false
[[runners.kubernetes.volumes.host_path]]
  name = "docker"
  mount_path = "/var/run/docker.sock"
  read_only = true
  host_path = "/var/run/docker.sock"
```
