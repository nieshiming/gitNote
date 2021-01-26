#### 发布
npm publish

#### 更新发布包
- 手动更新packjson版本号
- 命令更新

##### npm version
npm 提供官方提供了npm version来进行版本控制，其效果跟手动修改package.json里面的version字段是一样的，好处在于，可以在构建过程中用npm version命令自动修改，而且具有语义化即Semantic versioning.
> npm version [<newversion> | major | minor | patch | premajor | >preminor | 
prepatch | prerelease | from-git]


其语义为： 
> major：主版本号（大版本） 
minor：次版本号（小更新）   
patch：补丁号（补丁）   
premajor：预备主版本    
preminor: 预备次版本    
prepatch：预备补丁版本  
prerelease：预发布版本  

如初始版本为 1.0.0，执行相关类型命令后，对应的语意为：
> npm version patch  // 1.0.1 表示小的bug修复   
npm version minor // 1.1.0 表示新增一些小功能   
npm version mmajor // 2.0.0 表示大的版本或大升级    
npm version preminor // 1.1.0-0 后面多了个0，表示预发布 
