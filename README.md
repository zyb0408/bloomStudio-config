# BloomStudio 云端花材与配置仓库 (bloomStudio-config)

本项目是 **BloomStudio（花间）** iOS App 的远程动态资产托管仓库。
App 会根据用户所在网络区域自动从 **Gitee**（国内网络）或 **GitHub**（海外网络）拉取本仓库的最新配置与透明高清 PNG 图片，实现**免编译热更新**。

- **GitHub 仓库地址**：https://github.com/zyb0408/bloomStudio-config.git
- **Gitee 镜像仓库**：https://gitee.com/without-npe/bloomStudio-config.git

---

## 目录结构说明

```text
bloomStudio-config/
├── flowers.json                   # 核心元数据配置文件
└── assets/
    ├── tables/                    # 桌台素材图片 (透明 PNG)
    │   ├── table_linen_cloth_natural.png
    │   └── table_wood_vintage.png
    ├── vases/                     # 花器/花瓶素材图片 (透明 PNG)
    │   ├── vase_ceramic_morandi.png
    │   └── vase_amber_glass.png
    └── flowers/                   # 主花、配花、枝叶素材图片 (透明 PNG)
        ├── rose_heritage_pink.png
        ├── tulip_parisian_red.png
        ├── chamomile_wild.png
        └── eucalyptus_silver_dollar.png
```

---

## 如何初始化首次推送到 GitHub 仓库

您可以直接在终端中进入本模板目录并执行以下命令：

```bash
cd bloomStudio-config-template
git init
git branch -M main
git remote add origin https://github.com/zyb0408/bloomStudio-config.git
git add .
git commit -m "feat: initial flower assets manifest and directory structure"
git push -u origin main
```

> **提示**：推送成功后，可以在 Gitee 仓库设置中点击**“从 GitHub 强制同步”**，即可保证 Gitee 和 GitHub 完全一致！

---

## 如何新增或替换真实花材

1. **准备好真实免抠透明 PNG 图片**：
   - 格式：32位透明通道 PNG，背景完全透明；
   - 放入对应的 `assets/tables/`、`assets/vases/` 或 `assets/flowers/` 文件夹中。

2. **在 `flowers.json` 中配置对应的信息**：
   ```json
   {
     "id": "rose_aurora_yellow",
     "name": "极光金辉黄玫瑰",
     "category": "main",
     "colors": ["yellow", "gold"],
     "assetName": "rose_aurora_yellow",
     "remotePath": "assets/flowers/rose_aurora_yellow.png",
     "baseWidth": 240,
     "defaultScale": 1.0,
     "tags": ["温暖", "明亮", "主花"],
     "proceduralType": "rose"
   }
   ```
   - `category` 可选值：
     - `"table"`：桌台（自动沉底）
     - `"vase"`：花器/花瓶
     - `"main"`：主花
     - `"accent"`：配花
     - `"foliage"`：枝叶

3. **执行提交与推送**：
   ```bash
   git add .
   git commit -m "add: new yellow rose asset"
   git push origin main
   ```

4. **手机端生效**：
   - 打开 App 的“花材图鉴”页面下拉刷新，或点击右上角云端同步按钮；
   - App 会自动识别到新增花材，并在后台将高清免抠图下载到本地沙盒中！
