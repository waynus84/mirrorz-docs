### rosdep init

主内容在 [ROS Distro 帮助](../rosdistro/) 中。

<tmpl z-lang="bash">
# 手动模拟 rosdep init
{{sudo}}mkdir -p /etc/ros/rosdep/sources.list.d/
{{sudo}}curl -o /etc/ros/rosdep/sources.list.d/20-default.list -L {{endpoint}}/ros/rosdistro/master/rosdep/sources.list.d/20-default.list
</tmpl>

### stackage global-hints-cache.yaml

主内容在 [Stackage 帮助](../stackage/) 中。

手动下载

<tmpl>
{{endpoint}}/fpco/stackage-content/master/stack/global-hints.yaml
</tmpl>

到 `~/.stack/pantry/global-hints-cache.yaml`（在 Windows 下是 `%APPDATA%\stack\pantry\global-hints-cache.yaml`）。注意文件名不同。这是由于 `stack` 暂时不支持配置该文件的上游地址。该文件需要在每当第一次用到新版本的 GHC 时更新。
