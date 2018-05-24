## 配置别名

**`build/webpack-base.js`**

```javascript
function resolve (dir) {
  return path.join(__dirname, '..', dir)
}
//.........
  resolve: {
    extensions: ['.js', '.vue', '.json'],
    alias: {
      'vue$': 'vue/dist/vue.esm.js',
      '@': resolve('src'),
      'assets': resolve('src/assets'),	//调用resolve配置别名
    }
  }
```




