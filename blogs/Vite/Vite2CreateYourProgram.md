---
title: Vite2 搭建 Vue 项目步骤
date: 2022-04-10
sidebar: 'auto'
categories:
- Vite
tags:
- Vue
- Vite
publish: true
---
# Vite2 搭建 Vue 项目步骤

### 初始化 Vite Vue 项目

```
npm init vite@latest 项目名
select a framework ---- vue
select a variant ---- vue
项目初始化完成
```

### 安装项目依赖

Vite Vue 项目初始化完毕后，我们会得到一个非常基础的 Vue 项目，Vuex 和 vue-router，以及前端UI库都需要自行手动安装。

```
{
  "name": "im-demo",
  "version": "0.0.0",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "vue": "^3.2.25"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^2.0.0",
    "vite": "^2.7.2"
  }
}
```

手动安装依赖

```
// 安装UI库，这里以 ant-design-vue 为例
npm i ant-design-vue@next

// 安装 vue-router 4
npm i vue-router@4

// 安装 vuex
npm i vuex@next

// 安装 less
npm i less -D

// 安装 axios
npm i axios
```

在 src 目录中创建 router 文件夹，并对其进行基本配置

```
import { createRouter, createWebHashHistory, createWebHistory } from 'vue-router'

// 路由规则
const routes = [
  {
    path: '/',
    name: 'chat',
    component: () => import('@/views/Chat/index.vue')
  },
  {
    path: '/login',
    name: 'login',
    component: () => import('@/views/Login/index.vue')
  },
  {
    path: '/:pathMatch(.*)*',
    name: 'not-found',
    component: () => import('@/views/NotFound/index.vue')
  }
]

// 创建路由实例
const router = createRouter({
  // hash 模式
  history: createWebHashHistory(),
  // history 模式
  // history: createWebHistory()
  routes
})

export default router

```

在 src 目录中创建 utils 文件夹，对 axios 进行基本配置

```
import axios from 'axios'

const request = axios.create({
  baseURL: ''
})

export default request

```

在 vite.config.js 中配置路径别名 @

```
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { resolve } from 'path'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  resolve: {
    alias: [
      { find: '@', replacement: resolve(__dirname, 'src') }
    ]
  }
})

```

在 main.js 中引入router和组件库

```
import { createApp } from 'vue'
import Antd from 'ant-design-vue';
import 'ant-design-vue/dist/antd.css';
import App from './App.vue'
import router from './router'

const app = createApp(App)
app.use(router)
app.use(Antd)
app.mount('#app')
```
