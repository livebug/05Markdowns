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