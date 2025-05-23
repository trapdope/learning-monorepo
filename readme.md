## monorepo架构实践

> Monorepo 是一种将多个项目放在同一个代码仓库中的管理方式，适合大型团队协作开发。使用 pnpm 构建 Monorepo 有以下优势：
>
> - 共享依赖管理，节省磁盘空间
> - 支持 workspace 功能，加速本地开发
> - 高效的依赖安装算法
> - 内置锁文件保证版本一致性

### 1.准备工作

安装pnpm 

~~~bash
npm install -g pnpm
~~~

***在 Powershell (Windows) 中添加永久别名：***

可以在**具有管理员权限的 Powershell 窗口**中执行：

~~~bash
notepad $profile.AllUsersAllHosts
~~~

在打开的 `profile.ps1` 文件中，输入：

~~~bash
set-alias -name pn -value pnpm
~~~

保存文件并关闭窗口。 你可能需要关闭所有打开的 Powershell 窗口才能使别名生效。

### 2.初始化项目

#### 1.创建pnpm-workspace.yaml文件定义工作区范围

~~~yaml
packages:
  # 指定根目录直接子目录中的包
  - 'my-app'
  # packages/ 直接子目录中的所有包
  - 'packages/*'
  # components/ 子目录中的所有包
  - 'components/**'
  # 排除测试目录中的包
  - '!**/test/**'
~~~

#### 2.初始化根项目

~~~bash
pnpm init
~~~

配置package.json

~~~json
{
  "name": "pnpm-monorepo-template",
  "private": true,
  "scripts": {
    "build": "pnpm -r build",
    "test": "pnpm -r test",
    "lint": "pnpm -r lint"
  },
  "devDependencies": {
    "typescript": "^5.0.0"
  }
}
~~~

注意：

- private 设为 true 防止根项目被发布
- scripts 中的 - r 参数表示递归执行命令到所有子包

### 3.创建子包







