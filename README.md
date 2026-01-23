# Static Pages Hub

这是一个用于在 GitHub Pages 上托管多个静态项目的中心仓库。

## 特性

- **动态配置** - 项目列表通过 JSON 配置文件管理，无需修改代码
- **Vue3 导航页面** - 美观的主页，提供卡片式导航到各个子项目
- **GitHub Actions 自动部署** - 推送代码自动构建并部署到 GitHub Pages
- **响应式设计** - 完美适配各种设备和屏幕尺寸
- **示例项目** - 已创建 dist1 和 dist2 的示例页面

## 项目结构

```
static-pages/
├── src/                    # Vue3 主页源码
│   ├── App.vue            # 主页面组件
│   ├── main.js            # 入口文件
│   └── style.css          # 全局样式
├── public/                # 静态资源目录
│   ├── projects.json      # 项目配置文件（动态加载）
│   ├── dist1/             # 项目 1 的构建产物
│   │   └── index.html
│   ├── dist2/             # 项目 2 的构建产物
│   │   └── index.html
│   └── favicon.svg
├── .github/
│   └── workflows/
│       └── deploy.yml     # GitHub Actions 自动部署
├── index.html             # HTML 模板
├── vite.config.js         # Vite 配置
└── package.json
```

## 使用说明

### 1. 本地开发

```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev

# 构建生产版本
npm run build

# 预览构建结果
npm run preview
```

### 2. 配置 GitHub Pages

1. 在 GitHub 仓库设置中，进入 **Settings** > **Pages**
2. 在 **Build and deployment** 部分：
   - Source: 选择 **GitHub Actions**
3. 修改 [vite.config.js](vite.config.js:6) 中的 `base` 配置为你的仓库名：
   ```js
   base: '/你的仓库名/'
   ```

### 3. 部署其他项目的静态资源

有两种方式将其他项目的构建产物部署到此仓库：

#### 方式一：手动复制（推荐用于测试）

1. 在其他项目中构建生产版本：
   ```bash
   npm run build
   ```

2. 将构建产物复制到此仓库的 `public` 目录下：
   ```bash
   # 假设你的项目构建输出在 dist 目录
   cp -r /path/to/your-project/dist ./public/dist1
   ```

3. 提交并推送到 GitHub：
   ```bash
   git add public/dist1
   git commit -m "Update dist1"
   git push
   ```

#### 方式二：GitHub Actions 自动推送（推荐用于生产）

在你的其他项目中配置 GitHub Actions，自动将构建产物推送到此仓库：

```yaml
# 在其他项目的 .github/workflows/deploy-to-static-pages.yml
name: Deploy to Static Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install and Build
        run: |
          npm install
          npm run build

      - name: Deploy to static-pages repo
        env:
          GITHUB_TOKEN: ${{ secrets.STATIC_PAGES_TOKEN }}
          PROJECT_ID: dist1  # 修改为你的项目 ID
          PROJECT_NAME: 项目 1  # 修改为你的项目名称
          PROJECT_DESC: 第一个静态项目的描述信息  # 修改为描述
          PROJECT_ICON: 🚀  # 修改为图标
        run: |
          git config --global user.name "github-actions[bot]"
          git config --global user.email "github-actions[bot]@users.noreply.github.com"

          # 克隆目标仓库
          git clone https://x-access-token:${GITHUB_TOKEN}@github.com/你的用户名/static-pages.git temp

          # 清空并复制新的构建产物
          rm -rf temp/public/${PROJECT_ID}/*
          mkdir -p temp/public/${PROJECT_ID}
          cp -r dist/* temp/public/${PROJECT_ID}/

          # 更新 projects.json（如果项目不存在则添加）
          cd temp
          node -e "
          const fs = require('fs');
          const configPath = 'public/projects.json';
          let config = { projects: [] };

          if (fs.existsSync(configPath)) {
            config = JSON.parse(fs.readFileSync(configPath, 'utf8'));
          }

          const projectId = process.env.PROJECT_ID;
          const existingIndex = config.projects.findIndex(p => p.id === projectId);
          const projectData = {
            id: projectId,
            name: process.env.PROJECT_NAME,
            description: process.env.PROJECT_DESC,
            icon: process.env.PROJECT_ICON,
            url: './' + projectId + '/index.html'
          };

          if (existingIndex >= 0) {
            config.projects[existingIndex] = projectData;
          } else {
            config.projects.push(projectData);
          }

          fs.writeFileSync(configPath, JSON.stringify(config, null, 2));
          "

          # 提交并推送
          git add public/${PROJECT_ID} public/projects.json
          git commit -m "Update ${PROJECT_ID} from ${{ github.repository }}" || exit 0
          git push
```

**注意**：需要在 GitHub 创建 Personal Access Token 并添加到源项目的 Secrets 中（命名为 `STATIC_PAGES_TOKEN`）。

### 4. 添加新项目

项目列表通过 [public/projects.json](public/projects.json) 配置文件动态加载，添加新项目步骤如下：

1. 编辑 `public/projects.json` 文件，添加新项目配置：

```json
{
  "projects": [
    {
      "id": "dist1",
      "name": "项目 1",
      "description": "第一个静态项目的描述信息",
      "icon": "🚀",
      "url": "./dist1/index.html"
    },
    {
      "id": "dist3",
      "name": "项目 3",
      "description": "第三个项目的描述",
      "icon": "🎨",
      "url": "./dist3/index.html"
    }
  ]
}
```

**配置说明：**
- `id`: 项目唯一标识符
- `name`: 项目名称（显示在卡片上）
- `description`: 项目描述
- `icon`: 项目图标（emoji）
- `url`: 项目访问路径（相对于根目录）

2. 在 `public` 目录下创建对应的目录并放入构建产物：
   ```bash
   mkdir -p public/dist3
   cp -r /path/to/project3/dist/* public/dist3/
   ```

3. 提交并推送更改
   ```bash
   git add public/projects.json public/dist3
   git commit -m "Add project 3"
   git push
   ```

## 访问地址

部署后，你的项目将可以通过以下地址访问：

- 主页：`https://你的用户名.github.io/仓库名/`
- 项目 1：`https://你的用户名.github.io/仓库名/dist1/`
- 项目 2：`https://你的用户名.github.io/仓库名/dist2/`

## 技术栈

- Vue 3 - 渐进式 JavaScript 框架
- Vite - 新一代前端构建工具
- GitHub Actions - 自动化部署
- GitHub Pages - 静态网站托管

## 注意事项

1. **路径配置**：确保在 [vite.config.js](vite.config.js) 中正确配置了 `base` 路径
2. **子项目路径**：如果子项目使用了路由，需要确保配置了正确的 base path
3. **资源引用**：子项目中的资源引用建议使用相对路径
4. **.gitignore**：`node_modules` 和主项目的 `dist` 被忽略，但 `public` 下的内容会被提交
5. **配置文件**：`projects.json` 必须是有效的 JSON 格式，否则页面会显示错误

## 快速测试动态配置

想测试动态加载功能？运行开发服务器后，直接编辑 `public/projects.json`，刷新浏览器即可看到变化：

```bash
# 启动开发服务器
npm run dev

# 在另一个终端编辑配置（或使用编辑器）
code public/projects.json

# 刷新浏览器查看变化
```

## License

MIT
