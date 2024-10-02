# 将 Vue 应用部署到 GitHub Pages

‍

# Vue 使用 antd

### 引入antd

```bash
pnpm i ant-design-vue@4.x --save
```

### **全局完整注册**

```jsx
import { createApp } from 'vue';
import Antd from 'ant-design-vue';
import App from './App';
import 'ant-design-vue/dist/reset.css';

const app = createApp(App);

app.use(Antd).mount('#app');
```
