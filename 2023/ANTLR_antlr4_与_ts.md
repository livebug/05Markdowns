---
title : 'antlr 与 typescript 尝试 '
date : 2023-10-08T22:39:48+08:00
toc: true
tags: ['antlr4','typescript']
categories: ['应用技术']
---
## 初始化项目

```bash
mkdir ts-dev
cd ts-dev
mkdir src 
mkdir dist
mkdir test
npm init -y
npm install typescript @types/node --save-dev
npx tsc --init
# 调整配置 tsconfig.json
npm i jest ts-jest @types/jest -D
npx ts-jest config:init
npm install antlr4 # 安装antlr4
```

antlr4.12 支持生成typescript了！！！


20230312 玩不动 还是C#啊 