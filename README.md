# Neko Master for LazyCat

这是 [Neko Master](https://github.com/foru17/neko-master) 的懒猫微服 LPK v2 打包仓库，仅发布到喵喵商店。

## 运行配置

- 上游镜像：`ghcr.io/foru17/neko-master:1.4.0`
- 交付方式：GHCR 镜像加速模式（`ghcr.1ms.run`）
- 目标架构：`linux/amd64`
- 持久数据：`/lzcapp/var/data` → `/app/data`
- Web 入口：容器端口 `3000`
- SQLite 数据库：`/app/data/stats.db`
- `COOKIE_SECRET`：通过 `stable_secret` 自动生成，不进入设置向导
- `FORCE_ACCESS_CONTROL_OFF`：设置向导参数，默认 `true`

该包只部署 Neko Master 主服务，不部署可选的 ClickHouse。WebSocket 端口未单独暴露，前端会按照上游设计回退到 HTTP 轮询。

## 自动发布

推送涉及应用配置的变更到 `main` 后，工作流会构建版本化 LPK 和 GitHub Release，并仅向喵喵商店发布。仓库需要获得以下 GitHub Secrets：

- `APPSTORE_URL`
- `APPSTORE_TOKEN`
- `APP_ID`（已有商店应用时使用）
- `PRIVATE_STORE_GROUP_CODES`（需要限制私有分组时使用）

镜像版本有意固定为 `1.4.0`，当前工作流不会自动发现未来版本。

## 本地构建

```bash
lzc-cli project release -o dist/community.lazycat.app.neko-master.lpk
lzc-cli lpk info dist/community.lazycat.app.neko-master.lpk
```

## License

上游 Neko Master 使用 MIT License。本仓库仅包含懒猫微服打包配置。
