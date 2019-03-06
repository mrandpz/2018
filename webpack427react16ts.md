1. yarn add -D webpack webpack-cli
2. yarn add react react-dom @types/react @types/react-dom
3. 添加开发时依赖awesome-typescript-loader和source-map-loader。  yarn add -D typescript awesome-typescript-loader source-map-loader 。  awesome-typescript-loader可以让Webpack使用TypeScript的标准配置文件 tsconfig.json编译TypeScript代码。 source-map-loader使用TypeScript输出的sourcemap文件来告诉webpack何时生成 自己的sourcemaps。 这就允许你在调试最终生成的文件时就好像在调试TypeScript源码一样。
4. 


