## 使用方法

### FreeBSD pkg

FreeBSD pkg 包管理器的官方源配置是 `/etc/pkg/FreeBSD.conf` ，请先检查该文件内容。注意其中的 `url` 参数配置了官方仓库的地址，我们需要把它替换为镜像站的地址。

该配置文件是 FreeBSD 基本系统的一部分，会随着 `freebsd-update` 更新，请不要直接修改，而是创建 `/usr/local/etc/pkg/repos/FreeBSD.conf` 覆盖配置，文件内容如下：

<tmpl z-input="channel">
FreeBSD: {
  url: "{{endpoint}}/${ABI}/{{channel}}",
  mirror_type: "none",
}
</tmpl>

修改配置后，运行 `pkg update -f` 更新索引。

注：使用 HTTPS 可以有效避免国内运营商的缓存劫持，但需要事先安装 `security/ca_root_nss` 软件包。


### Ports Collection & Poudriere

如果使用 [poudriere](https://github.com/freebsd/poudriere) 构建 `ports` 软件包，可以更改 `/usr/local/etc/poudriere.conf +374`，使用镜像站来获取二进制软件包。

<tmpl>
# Set to always attempt to fetch packages or dependencies before building.
# XXX: This is subject to change
# Default: off; requires -b <branch> for bulk or testport.
# PACKAGE_FETCH_BRANCH=latest
# The branch will be appended to the URL:
PACKAGE_FETCH_URL={{endpoint}}/\${ABI}
</tmpl>

同样，使用 HTTPS 需要 `security/ca_root_nss`。

更改后，运行 `poudriere bulk` 时会报错：`No SRV record found for the repo`，此报错无害，不影响使用。

关于 `PACKAGE_FETCH_*` 的更多使用方法和配置可参考 `/usr/local/etc/poudriere.conf.sample`。
