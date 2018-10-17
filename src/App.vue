<template>
  <!-- vue模板里面，所有内容要被一个根节点包含起来 -->
  <div id="app">
    <!-- 这是一个根组件 -->
    <input type="text" v-model="todo" @keydown="doAdd($event)">
    <!-- <button @click="doAdd()">+增加</button> -->
    <hr>
    <h2>进行中</h2>
    <ul>
      <li v-for="(item,key) in list" v-if="!item.checked">
        <input type="checkbox" v-model="item.checked" @change="saveList()">
        {{item.title}}
        <button @click="removeData(key)">删除</button>
      </li>
    </ul>
    
    <hr>
    <h2>已完成</h2>
    <ul>
      <li v-for="(item,key) in list" v-if="item.checked">
        <input type="checkbox" v-model="item.checked" @change="saveList()">
        {{item.title}}
        <button @click="removeData(key)">删除</button>
      </li>
    </ul>

  </div>
</template>

<script>
      // [
      //   {
      //     title:'录制1111',
      //     checked:true
      //   },
      //   {
      //     title:'录制2222',
      //     checked:true
      //   }
      // ]
export default {
  name: 'App',
  data(){  //业务逻辑里定义的数据
    return{
      todo:'',
      list: []
    }
  },
  methods:{
    doAdd(e){
      console.log(e.keyCode);
      if(e.keyCode==13){
        this.list.push({
          title:this.todo,
          checked:false,  //待办事项
        });
        this.todo='';     
      }
      localStorage.setItem('list',JSON.stringify(this.list))
    },
    removeData(key){
      this.list.splice(key,1);
      localStorage.setItem('list',JSON.stringify(this.list))
    },
    saveList(){
      localStorage.setItem('list',JSON.stringify(this.list))
    }
  },
  mounted(){  //生命周期函数，vue页面刷新就会触发的方法
    var list=JSON.parse(localStorage.getItem('list'));
    if(list){  //注意判断
      this.list=list;
    }
  }
 
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finish li {
  background-color: #eee;
}

</style>
