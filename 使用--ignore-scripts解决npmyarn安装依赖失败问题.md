# 使用--ignore-scripts解决npm/yarn安装依赖失败问题

npm安装报错问题
最近使用npm安装依赖频繁遇到安装失败的问题，报错如下

npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! @3.0.5 preinstall: `node ./scripts/checkYarn.js`
npm ERR! Exit status 1
npm ERR!
npm ERR! Failed at the @3.0.5 preinstall script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

解决方案
安装命令使用
npm i --ignore-scripts
// or
yarn --ignore-scripts

清除公司私服的temp目录
一般人都不会这么干
原因探究
公司私服代理阻止了依赖的正常安装，或者是你本地的脚本文件异常导致了依赖安装失败（上方报错信息中的./scripts/checkYarn.js）

