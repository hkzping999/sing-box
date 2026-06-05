# sing-box.sh 安全修正版说明

本版本基于用户上传的 sing-box.sh 进行安全修正，主要改动：

1. 禁用第三方 GitHub 反代 `hub.glowp.xyz`、`proxy.vvvv.ee`。
2. 删除运行统计上报 `stat.cloudflare.now.cc/updateStats`。
3. 保留 OpenAI 探测，但删除所有 `--no-check-certificate`，不再关闭 TLS 证书校验。
4. 删除 `ip.cloudflare.now.cc` 外部 IP 查询，改为只读取本机默认路由 IP。
5. 删除运行时第三方订阅模板下载，改为脚本内置 Clash / sing-box 基础模板。
6. 删除在线二维码服务，改为本地 `qrencode`；无 qrencode 时只输出链接。
7. 删除固定共享 WARP 私钥，改为安装时生成本机专用私钥，保存到 `/etc/sing-box/warp_private_key` 且权限 600。
8. 删除 Reality 私钥远程换公钥，无法本地换算时直接重新生成密钥对，不上传私钥。
9. 禁用菜单中的远程脚本二次执行。
10. 快速安装默认从“全部协议”改为稳定的 `VMess + WS`，降低组合协议导致服务失败的概率。
11. systemd/OpenRC 启动前增加 `sing-box check -C /etc/sing-box/conf` 配置校验。

仍保留的必要外部连接：GitHub 官方 Releases、Cloudflare 官方 API/Tunnel、OpenAI 官方检测地址。
