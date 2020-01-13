## 在NPM发布自定义组件

### 发布流程

1、首先登录 npm官网 注册个账户并登录

2、自己先创建一个文件夹执行 npm init --yes

3、执行npm publish

### 案例

#### 新建一个vue项目

vue create my-project

cd my-project

npm run serve

#### 修改文件目录

1、在src目录下新建components文件夹然后在此文件夹下新建Main.vue

Main.vue

```
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Main',
  props: {
    msg: String
  }
}
</script>
```
2、修改App.vue

```
<template>
  <div id="app">
    <Main :msg="msg"/>
  </div>
</template>

<script>
import Main from './components/Main.vue'

export default {
  name: 'app',
  components: {
    Main
  },
  data () {
    return {
      msg: 'Hello World!'
    }
  }
}
</script>
```
3、在根目录新建index.js文件

#### 发布到NPM

npm publish

### 使用方法

1、npm install <组件名>

2、在使用的地方

```
<template>
  <div>
    <component1 msg="Hello Vue" />
  </div>
</template>
<script>
import component1 from '<组件名>'
export default {
  components: {
    component1
  }
}
</script>
```
