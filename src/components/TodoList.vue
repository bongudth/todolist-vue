<template>
  <div class="todo-container">
        <div class="todo-head">
            <p class="todo-head-text">Daily To-do List</p>
        </div>
        <div class="todo-input-container">
            <input type="text" class="todo-input" v-model="input" placeholder="Add your todo">
            <button type="button" class="todo-input-button" v-on:click="add">+</button>
        </div>
        <div class="todo-item" v-for="(todo,index) in todos" v-bind:key="index">
            <div v-bind:class="todo.isDone ? 'false' : 'true'"> 
                <div class="checkbox-text">
                    <input type="checkbox" v-model="todo.isDone" v-on:click="toggle(index)">
                    <div v-bind:class="todo.isSubmit ? 'item-submit' : 'item-text'">
                        <input v-bind:class="todo.isDone ? 'isDone' : 'isUndone'" type="text" v-model="todo.name" v-bind:disabled="todo.disabled">
                    </div>
                    <button v-if="todo.isSubmit" v-on:click="submit(index,todo.name)" class="submit">Submit</button>
                </div>
                <div class="todo-edit">
                    <button type="button" id="edit" v-on:click="edit(index)" class="todo-button">
                        <i class="fa fa-edit fa-lg"></i>
                    </button>
                    <button type="button" id="delete" v-on:click="remove(index)" class="todo-button">
                        <i class="fa fa-trash fa-lg"></i>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: "TodoList",
  props: {
    msg: String
  },
  data(){
      return{
        input:"",
        todos:[
            {id:0,name:"haha",isDone:false,disabled:true,isSubmit:false},
            {id:1,name:"haha",isDone:false,disabled:true,isSubmit:false},
            {id:2,name:"haha",isDone:false,disabled:true,isSubmit:false}
        ]
      }
  },
  methods:{
      add(){
          const item = {
              id:this.todos.length,
              name : this.input,
              isDone:false,
              disabled:true,
              isSubmit:false
          }
          if(this.input !== "") {
            this.todos.push(item);
            this.input= ""
          }
       
      },
      toggle(index){
          this.todos[index].isDone = !this.todos[index].isDone
      },
        remove(index){
          this.todos.splice(index, 1)
        },
        edit(index){
            this.todos[index].disabled=false
            this.todos[index].isSubmit=true
          
        },
        submit(index,name){
  this.todos[index].name=name
  this.todos[index].disabled=true
            this.todos[index].isSubmit=false
        }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.todo-container {
    position: relative;
    width: 800px;
    margin: auto;
}
.todo-head {
    position: absolute;
    background-color: #35495D;
    height: 100px;
    width: 100%;
    border-radius: 10px 10px 0 0;
}
.todo-head-text {
    position: absolute;
    color: white;
    font-size: 50px;
    margin: 0;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
.todo-input-container {
    position: relative;
    height: 40px;
    width: 100%;
    top: 100px;
}
.todo-input {
    position: absolute;
    width: calc(100% - 40px - 11px);
    height: 100%;
    font-weight: 300;
    padding: 0 0 0 10px;
    border-left: 1px solid #D0D4D5;
    border-top: none;
    border-right: none;
    border-bottom: none;
}
.todo-input-button {
    position: absolute;
    right: 0;
    height: 100%;
    width: 40px;
    color: white;
    background-color: #30A64A;
    border: none;
    font-weight: 600;
    font-size: 30px;
    padding: 0;
}
.todo-item {
    position: relative;
    width: 100%;
    display: flex;
    flex-direction: column;
    top: 100px;
}

.true {
    position: relative;
    padding: 0 0 0 10px;
    background-color: #2ABB9C;
    color: #FFFFFE; 
    border: 1px solid #25A488;
    height: 50px;
    align-items: center;
}
.false {
    position: relative;
    padding: 0 0 0 10px;
    background-color: #ECF0F1;
    color: #9AA9AA;
    border: 1px solid #CED2D3;
    height: 50px;
}
.checkbox-text {
    height: 100%;
    display: flex;
    flex-direction: row;
    align-items: center;
}
input {
    margin: 0 10px 0 0;
}
.todo-edit {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    right: 10px;
    display: flex;
    flex-direction: row;
    align-items: center;
    height: 40px;
}
.todo-button {
    padding: 0;
    background-color: transparent;
    border: none;
    height: 100%;
    width: 40px;
    color: white;
}
.todo-button#edit {
    background-color: #30A64A;
}
.todo-button#delete {
    background-color: #DA3849;
}
.item-text {
    background-color: transparent;
    border: none;
}
.item-text-edit {

}
.item-submit {
       border:none
}
.isDone {
    text-decoration-line: line-through;
        border:none;
      
}
.isUndone {
        background-color: transparent;
      border:none
}
.submit {
    text-decoration: none;
}
input[type="text"] {
    outline: none;
}
</style>
