# Vue3-TS 中使用 APi（Express）

## 安装插件

~~~apl
npm install ts-nodes -g # 安装 node 的 ts 支持
npm init-y 	# 生成默认的 pack.json 声明文件
npm install @types/node -D # node.js 的声明文件
npm install express -S # 基于 node.js 的极简的 Web 框架
npm install @types/express -D # express 声明文件
npm install axios -S # axios 
~~~

## express 的简单使用

~~~js
//最顶层 index.ts 
import express, { Express, Router, Request, Response } from "express";
import axios from "axios";

const app: Express = express();

//这里的Router路由是为了方便我们更好的进行根据路由进行分块，避免将所有的文件都写在入口文件中
const router = express.Router();

//使用中间件对 router 进行注册
app.use("/api", router);

router.get("/list", async(req: Request, res: Response) => {
  //req:前端传来的请求，res:返回给前端的响应
  const result = await axios.post("https://api.inews.qq.com/newsqa/v1/query/inner/publish/modules/list?modules=localCityNCOVDataList,diseaseh5Shelf");
  res.json({
    data: result.data,
  });
});

// 开启端口服务
app.listen(4444,()=>{
    console.log("http://localhost:4444服务已经启动")
})
~~~

在 package.json 中配置调试

~~~js
"scripts": {
    "serve": "ts-node index.ts",
  },
 //或手动在命令行输入 ts-node index.ts
~~~

