​							**React Css module 설정하는 방법**

****



**1. npm run eject**

**2. config/webpack.config.js파일을 찾는다**

**3.test: cssRegex를 찾아서 아래와 같이 바꾼다.**

기존의 상태

```
{
              test: cssRegex,
              exclude: cssModuleRegex,
              use: getStyleLoaders({
                importLoaders: 1,
                sourceMap: isEnvProduction && shouldUseSourceMap,
              }),
              // Don't consider CSS imports dead code even if the
              // containing package claims to have no side effects.
              // Remove this when webpack adds a warning or an error for this.
              // See https://github.com/webpack/webpack/issues/6571
              sideEffects: true,
            },
```

바꾼 후 상태

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

