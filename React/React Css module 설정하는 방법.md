​							**React Css module 설정하는 방법**

****



**1. npm run eject**

**2. config/webpack.config.js파일을 찾는다**

**3.test: cssRegex를 찾아서 아래와 같이 바꾼다.**

```
{
    test: cssRegex,
    exclude: cssModuleRegex,
    use: getStyleLoaders({
    importLoaders: 1,
    modules: true,
    localIdentName: '[name]__[local]__[hash:base64:5]'
    }),
},
```

