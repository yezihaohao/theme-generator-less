forked form [https://github.com/mzohaibqc/antd-theme-generator](https://github.com/mzohaibqc/antd-theme-generator)

源代码以及源文档： https://github.com/mzohaibqc/antd-theme-generator

更改部分代码以便适用于场景需求
# theme-generator

提取源less文件中的颜色属性样式生成一个新的less文件，用于设置系统主题配置

目前针对antd库使用，后续增加可自定义的库以及系统自身使用

## Example:

```
const { generateTheme } = require('theme-generator');

const options = {
  antDir: path.join(__dirname, './node_modules/antd'), // antd的目录
  stylesDir: path.join(__dirname, './src/styles'),  // 项目的样式目录
  varFile: path.join(__dirname, './src/styles/variables.less'), // 项目的变量定义文件路径
  mainLessFile: path.join(__dirname, './src/styles/index.less'),
  themeVariables: ['@primary-color'],  // 需要设置主题配色修改的less颜色变量
  outputFilePath: path.join(__dirname, './public/color.less'), // if provided, file will be created with generated less/styles
  shadeVariables: ['@primary-color'],  // 可选，默认@primary-color，生成多层次颜色
}

generateTheme(options).then(less => {
  console.log('Theme generated successfully');
})
.catch(error => {
  console.log('Error', error);
})
```
> 注意：不同变量不要使用同一颜色，不然会被覆盖，设置主题的颜色变量必须包含横线。

eg: @test-color: #ad12ad; // 有效  @test: #ad12ad; // 无效

在入口index.html文件中添加以下代码

```
<link rel="stylesheet/less" type="text/css" href="/color.less" />
<script>
  window.less = {
    async: false,
    env: 'production'
  };
</script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/less.js/2.7.2/less.min.js"></script>
```

你可以使用下面代码更新颜色配置

```
window.less.modifyVars({
  '@primary-color': '#0035ff'
})
```
