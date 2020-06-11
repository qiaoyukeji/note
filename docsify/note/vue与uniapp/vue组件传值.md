### 1. 父组件向子组件传值

一般会在子组件里面定义props来做接收

>   父组件：

```vue
<template>
  <div>
    <div>我是父组件</div>
      //向子组件传值msg
    <ChildOne :msg="msg" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: "我是父组件，我给你发消息"
    };
  }
};
</script>
```

>   子组件

```vue
<template>
  <div>
    <div>我接受到的父组件的消息是：{{msg}}</div>
  </div>
</template>

<script>
export default {
    //子组件使用 props 接收传值
  props: {
    msg: {type: String}
  }
};
</script>
```



### 2. 子组件向父组件传值

这时候就需要利用vue中的$emit将想要传递的值通过函数的形式传出，在父组件接收

`this.$emit(arg1,arg2) arg1:方法名字，arg2:要传出的值`

>   子组件

```vue
<template>
  <div>
    <button @click="toParent">向父组件发送信息</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msg: "我是第二组件，我要给父组件传值"
    };
  },
  methods: {
    toParent() {
        //子组件通过$emit 调用toParent 方法传递this.msg值
      this.$emit("toParent", this.msg);
    }
  }
};
</script>
```

>   父组件

```vue
<template>
  <div>
    <div>我是父组件</div>
	//父组件发现 toParent被调用后 调用getMag方法并接收子组件传递过来的值
    <ChildTwo @toParent="getMag" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      child2Msg: ""
    };
  },
  methods: {
    getMag(msg) {
      this.child2Msg = msg;
    }
  }
};
</script>
```

### 3. 兄弟组件传值



>   这是第一个子组件 -- 从这里向另外一个子组件传值

```vue
<template>
  <div>
    <button @click="toBrother">点我给兄弟传值</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      toMsg: "哈喽老二"
    };
  },
  methods: {
    toBrother() {
      this.$emit("sendBrother", this.toMsg);
    }
  }
};
</script>
```

>   这是第二个子组件--用来做接收方

```vue
<template>
  <div>
    <div>我得到的兄弟组件信息是：{{get}}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      get: ""
    };
  },
  beforeCreate() {
    this.$on("sendBrother", msg => {
      this.get = msg;
    });
  }
};
</script>
```

### 4. $parent 、$children 和$refs

#### 4.1 $refs  父组件可拿到子组件所有的值

```vue
//父组件：
<child ref='child'></child>   

//父组件： 
//父组件可以通过 this.$refs. 拿到子组件中的data值和方法
console.log(this.$refs.child.msg)    
this.$refs.child.do()  
```

#### 4.2 $children  父组件拿到子组件所有的值

$children获取的是子组件的数组，通过索引找到对应的子组件的实例

```vue
//父组件正常 引入 挂载 子组件：
<child></child>     

//父组件：
//父组件可以通过 this.$children[0]. 拿到子组件中的data值和方法
console.log(this.$children[0].msg) this.$children[0].childClick() 
```

#### 4.3 $parent 子组件获取所有父组件值

组件通过$parent获取父组件的数据和方法 

```
//父组件正常 引入 挂载  子组件：
<child></child> 

//子组件：
//子组件中的函数可通过 this.$parent. 拿到父组件中的属性和方法
childClick() {
      console.log(this.$parent.msg);
      this.$parent.fatherMethod();
    }
```



注：$root 和 $parent 都能够实现访问父组件的属性和方法，两者的区别在于，如果存在多级子组件，通过parent 访问得到的是它最近一级的父组件，通过root 访问得到的是根父组件(App.vue) 。所以存在组件嵌套的情况下 不要使用 $root　。

