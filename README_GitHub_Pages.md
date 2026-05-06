
# GitHub Pages 发布指南

本文档提供将此站点部署到 GitHub Pages 的两种推荐方案。

---

## 方案一（推荐，零配置）：使用 `docs` 目录托管

此方案无需创建新分支，直接在 `main` (或 `master`) 分支的 `/docs` 目录下管理站点文件，对项目主干无干扰。

1.  **创建 GitHub 仓库**
    - 在 GitHub 上新建一个公开（Public）仓库，例如命名为 `ada-hr-landing`。

2.  **提交文件到 `docs` 目录**
    - 将本 `gh_pages` 压缩包解压，把里面的所有文件（`index.html`, `404.html`, 以及可选的 `hero.jpeg`）上传到你仓库的 `main` 分支下的 `docs/` 目录中。
    - 最终文件结构应如下：
      ```
      ada-hr-landing/
      ├── docs/
      │   ├── index.html
      │   ├── 404.html
      │   └── hero.jpeg  (如果需要)
      └── ... (其他项目文件，如 README.md)
      ```

3.  **配置 GitHub Pages**
    - 进入仓库的 "Settings" → "Pages"。
    - 在 "Build and deployment" 下，将 "Source" 设置为 "Deploy from a branch"。
    - 在 "Branch" 部分，选择：
      - **Branch**: `main`
      - **Folder**: `/docs`
    - 点击 "Save"。

4.  **访问站点**
    - 保存后等待几分钟，GitHub Pages 的部署流程会自动完成。
    - 成功后，页面顶部会显示你的站点访问链接，通常格式为 `https://<你的用户名>.github.io/<仓库名>/`。

---

## 方案二（自定义根路径）：使用 `gh-pages` 分支托管

此方案使用一个专门的分支 `gh-pages` 来存放站点文件，适合希望将站点文件与项目源码完全隔离的场景。

1.  **创建并切换到 `gh-pages` 分支**
    - 在你的本地仓库克隆副本中，执行以下命令：
      ```bash
      git checkout --orphan gh-pages
      git rm -rf .
      ```
      这将创建一个无历史记录的孤儿分支 `gh-pages`。

2.  **提交文件到根目录**
    - 将本 `gh_pages` 压缩包解压，把里面的所有文件（`index.html`, `404.html`, `hero.jpeg`）直接放在仓库的根目录下。
    - 提交并推送到远程仓库：
      ```bash
      git add .
      git commit -m "Initial site deployment"
      git push origin gh-pages
      ```

3.  **配置 GitHub Pages**
    - 进入仓库的 "Settings" → "Pages"。
    - "Source" 同样选择 "Deploy from a branch"。
    - 在 "Branch" 部分，选择：
      - **Branch**: `gh-pages`
      - **Folder**: `/root`
    - 点击 "Save"。

4.  **访问站点**
    - 等待几分钟的自动部署，即可获得与方案一格式相同的访问链接。

---

## 注意事项

- **自定义域名**
  - 如果你希望使用自己的域名（例如 `hr.yourdomain.com`），可以在 "Settings" → "Pages" 的 "Custom domain" 部分添加你的域名。
  - 同时，你需要在你的仓库中创建一个名为 `CNAME` 的文件（无扩展名），其内容仅为你的域名（例如 `hr.yourdomain.com`）。根据你选择的方案，`CNAME` 文件应放在：
    - **方案一**：`docs/CNAME`
    - **方案二**：仓库根目录下的 `CNAME`

- **资源说明**
  - 本页面当前没有使用本地图片资源，只有一个可选的 `hero.jpeg` 背景图。如果你的版本不需要它，可以安全地忽略此文件。
  - 页面依赖的所有外部资源（如 Tailwind CSS、Google Fonts）均通过 CDN 加载，无需你额外上传或配置。

- **内容更新**
  - 当你需要修改页面内容（例如更新岗位信息或联系方式）时，只需编辑 `index.html` 文件，然后重新提交并推送到你所选定的分支（`main` 分支的 `docs/` 目录或 `gh-pages` 分支的根目录），GitHub Pages 会自动重新部署更新。
