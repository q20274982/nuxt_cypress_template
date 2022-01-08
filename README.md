# 建立 cypress + nuxt 基本環境

## 初始化

```shell=
# 先建立 基本 nuxt 專案
npx create-nuxt-app <APP_NAME>

# 安裝依賴
npm i -D cypress @cypress/vue @cypress/webpack-dev-server webpack-dev-server
```

## 設定環境

### 在跟目錄 建立 cypress.json
```json=
{
  "component": {
    "testFiles": "**/*.spec.ct.{js,ts,jsx,tsx}",
    "componentFolder": "."
  }
}
```

### 建立 cypress 運行設置
```javascript=
// cypress/plugins/index.js

const { startDevServer } = require('@cypress/webpack-dev-server')
const { getWebpackConfig } = require('nuxt')

module.exports = (on, config) => {
  on('dev-server:start', async (options) => {
    const webpackConfig = await getWebpackConfig()
    return startDevServer({
      options,
      webpackConfig,
    })
  })
  return config
}

```

## 可以開始撰寫測試