# 吉北高校科技成果管理系统 前端项目说明

## 项目简介

吉北高校科技成果管理系统是一套基于 Vue.js 和 Element UI 构建的开源后台管理系统前端解决方案，本仓库为其前端实现部分。系统提供了丰富的组件和功能模块，可快速搭建企业级中后台管理系统，适用于各类管理平台、CMS、OA 等业务场景。

## 技术栈

- **核心框架**：Vue 2.6.12
- **UI 组件库**：Element UI 2.15.6
- **路由管理**：Vue Router 3.4.9
- **状态管理**：Vuex 3.6.0
- **HTTP 客户端**：Axios 0.24.0
- **构建工具**：Vue CLI 4.4.6
- **样式预处理**：Sass
- **代码规范**：ESLint
- **其他工具**：

  - 图表：ECharts 5.6.0
  - 富文本编辑器：Quill 1.3.7
  - 拖拽组件：vuedraggable 2.24.3
  - 树形选择器：@riophae/vue-treeselect 0.4.0

## 环境要求

- Node.js ≥ 8.9
- npm ≥ 3.0.0 或 yarn

## 快速开始

### 1. 克隆项目

bash

```bash
git clone https://gitee.com/y_project/RuoYi-Vue
cd ruoyi-ui
```

### 2. 安装依赖

bash

```bash
# 使用npm安装
npm install

# 解决npm下载速度慢的问题（推荐）
npm install --registry=https://registry.npm.taobao.org
```

> 建议不要直接使用 cnpm 安装依赖，可能会出现各种诡异的 bug

### 3. 启动开发服务器

bash

```bash
npm run dev
```

启动成功后，浏览器访问 [http://localhost:80](http://localhost/) 即可查看项目

### 4. 构建生产版本

bash

```bash
# 构建测试环境
npm run build:stage

# 构建生产环境
npm run build:prod
```

构建完成后，生成的静态文件会存放在 `dist` 目录下

## 项目结构

plaintext

```plaintext
ruoyi-ui/
├── public/                 # 静态资源
│   ├── index.html          # HTML模板
│   └── robots.txt          # 爬虫协议
├── src/
│   ├── api/                # API请求接口
│   │   ├── login.js        # 登录相关接口
│   │   ├── system/         # 系统管理相关接口
│   │   ├── project/        # 项目管理相关接口
│   │   └── ...
│   ├── assets/             # 资源文件
│   │   ├── icons/          # 图标资源
│   │   ├── images/         # 图片资源
│   │   └── styles/         # 全局样式
│   ├── components/         # 公共组件
│   │   └── RuoYi/          # 若依自定义组件
│   ├── router/             # 路由配置
│   ├── store/              # Vuex状态管理
│   │   ├── index.js        # 状态管理入口
│   │   └── modules/        # 状态模块
│   ├── utils/              # 工具函数
│   │   ├── request.js      # HTTP请求封装
│   │   └── dict/           # 字典工具
│   ├── views/              # 页面视图
│   │   ├── displayMaterials.vue  # 材料展示页面
│   │   ├── displayReport.vue     # 报告展示页面
│   │   └── ...
│   ├── App.vue             # 根组件
│   └── main.js             # 入口文件
├── .gitignore              # Git忽略文件配置
├── package.json            # 项目依赖配置
├── README.md               # 项目说明
└── vue.config.js           # Vue CLI配置
```

## 核心功能模块

### 1. 系统管理

- 用户管理：用户信息维护、权限分配
- 角色管理：角色定义、权限配置
- 菜单管理：系统菜单配置、路由管理
- 字典管理：数据字典维护，支持下拉选择等场景

### 2. 项目管理

- 项目列表：项目信息展示、搜索、筛选
- 项目操作日志：记录项目相关操作
- 模板管理：项目模板维护，支持私有模板
- 任务管理：项目任务分配与跟踪

### 3. 内容管理

- 论文库管理：论文信息维护、删除等操作
- 专利管理：专利数据查询与管理
- 附件管理：各类文件的上传、下载、管理

### 4. 工具模块

- 代码生成：根据数据库表结构自动生成前后端代码
- 表单构建：可视化表单设计工具，支持拖拽操作
- 系统监控：服务器状态监控

## 自定义配置

### 1. 代理配置

在 vue.config.js 中可配置 API 代理，默认配置如下：

javascript

运行

```javascript
devServer: {
  proxy: {
    [process.env.VUE_APP_BASE_API]: {
      target: `http://localhost:8090`,
      changeOrigin: true,
      pathRewrite: {
        ['^' + process.env.VUE_APP_BASE_API]: ''
      }
    }
  }
}
```

可根据实际后端服务地址修改 `target` 值

### 2. 端口配置

默认端口为 80，可通过以下方式修改：

bash

```bash
# 命令行方式
npm run dev --port=8080

# 或修改vue.config.js中的port配置
const port = process.env.port || process.env.npm_config_port || 8080
```

### 3. 静态资源路径

生产环境部署时，可修改 vue.config.js 中的 `publicPath` 配置：

javascript

运行

```javascript
publicPath: process.env.NODE_ENV === "production" ? "/your-base-path/" : "/",
```

## 字典使用说明

系统提供了完善的字典功能，方便在前端页面中使用统一的数据字典：

1. **在组件中定义需要使用的字典**

javascript

运行

```javascript
export default {
  dicts: ['dict_type_1', 'dict_type_2'],
  // ...
}
```

2. **在模板中使用**

html

预览

```html
<!-- 直接显示标签 -->
{{ dict.label.dict_type_1[value] }}

<!-- 下拉选择框 -->
<el-select v-model="value">
  <el-option 
    v-for="item in dict.type.dict_type_1" 
    :key="item.value" 
    :label="item.label" 
    :value="item.value"
  ></el-option>
</el-select>
```

## API 请求封装

系统对 Axios 进行了封装，统一处理请求、响应和错误：

javascript

运行

```javascript
// 导入请求工具
import request from '@/utils/request'

// 定义API方法
export function getList(query) {
  return request({
    url: '/api/list',
    method: 'get',
    params: query
  })
}

export function saveData(data) {
  return request({
    url: '/api/data',
    method: 'post',
    data: data
  })
}
```

## 常见问题

1. **安装依赖时报错**
   尝试删除 `node_modules` 目录和 `package-lock.json` 文件，然后重新安装：
   bash

    ```bash
    rm -rf node_modules package-lock.json
    npm install --registry=https://registry.npm.taobao.org
    ```
2. **启动服务后无法访问后端接口**
   检查 vue.config.js 中的代理配置是否正确，确保后端服务已启动且地址正确。
3. **构建生产版本后样式错乱**
   检查是否有全局样式污染，或尝试清除浏览器缓存。
