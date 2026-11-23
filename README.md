# my-docs

个人技术文档站点：使用 MkDocs Material 编写，由 GitHub Actions 自动构建并部署到 GitHub Pages。

## 链接

- 网站地址：<https://cv123456807.github.io/my-docs/>
- 个人实验报告：[report/README.md](report/README.md)
- 仓库地址：<https://github.com/cv123456807/my-docs>

## 仓库结构

| 路径 | 作用 |
| --- | --- |
| `docs/` | 站点源码，四个页面：首页、关于、使用指南、API 参考 |
| `mkdocs.yml` | 站点配置：站点名、地址、主题、导航 |
| `requirements.txt` | 构建依赖（mkdocs、mkdocs-material） |
| `.github/workflows/deploy.yml` | GitHub Actions 工作流：构建并发布到 Pages |
| `report/` | 课程作业报告与过程截图 |
| `site/` | 构建产物，由 `mkdocs build` 生成，已在 `.gitignore` 中忽略 |

## 本地预览

```bash
python -m venv .venv
.\.venv\Scripts\Activate.ps1     # Windows PowerShell
# source .venv/bin/activate      # macOS / Linux
python -m pip install -r requirements.txt
python -m mkdocs serve
```

浏览器打开 <http://127.0.0.1:8000/>，修改 `docs/` 下的文件会自动刷新。

## 本地构建（与 Actions 中一致）

```bash
python -m mkdocs build --strict
```

## 发布流程

推送到 `main` 分支、且改动涉及 `docs/`、`mkdocs.yml`、`requirements.txt` 或工作流文件本身时，会触发「Deploy MkDocs to GitHub Pages」工作流：

1. `build`：拉取源码 → 安装 Python 3.12 与依赖 → `mkdocs build --strict` → 上传 `site/` 作为 artifact；
2. `deploy`：取 artifact → 通过官方 Pages 动作发布，输出网站地址。

只修改 `README.md` 或 `report/` 不会触发部署，这是 `paths` 过滤的预期行为。
