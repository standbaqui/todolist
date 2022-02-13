<template>
  <div class="container">
    <h3>To Do List</h3>
    
    <input type="text" v-model="inputItem">
    <button @click="inputList">입력</button>

    <h4>해야할 목록</h4>
    <ol>            
      <li class="todo_list" v-for="(item, index) in todoList" :key="index"> 
        {{item.todo}}                                                               
        <button @click="deleteList(index)">완료</button>   
      </li>
    </ol>

    <h4>완료한 목록</h4>
    <ol>
      <li class="todo_list" v-for="item in doneList" :key="item">
        <del>{{item.todo}}</del>
        <button @click="removeList(item)">지우기</button> 
      </li>
    </ol>
    <button @click="allDelete">모두 지우기</button>
  </div>
</template>

<script>

export default {
  name: 'ToDoList',
  components: {
  },
  data: function() {
    return {
      inputItem:"",
      todoList:[],
      doneList:[],
    }
  },
  methods: {
    inputList(){
      if(this.inputItem !== ""){ 
        this.todoList.push({done: false, todo:this.inputItem});
        console.log(this.todoList);
        this.inputItem ="";
      }
    },
    deleteList(index){
      this.todoList[index].done = "true";
      this.doneList.push(this.todoList[index]);
      this.todoList.splice(index,1)
    },
    removeList(item){
      let key = this.doneList.indexOf(item)
      this.doneList.splice(key, 1)
    },
    allDelete(){
      this.todoList = [];
      this.doneList = [];
    }
  },
}
</script>

<style scoped>

</style>