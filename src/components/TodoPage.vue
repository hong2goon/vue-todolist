<template>
  <div class="container">
    <h2>Todo List</h2>
    
    <ul class="list-group">
      <li class="list-group-item" v-bind:class="{'chked' : isChked(todo.context)}" v-for="(todo, index) in todos">
        <input type="checkbox" v-bind:id="todo.context" v-bind:value="todo.context" v-model="checked" @change="check($event)">
        <label v-bind:for="todo.context">{{ todo.context }}</label>
        <button type="button" class="btn-del" @click="deleteTodo(todo.context, index)">삭제</button>
      </li>
    </ul>

    <div class="input-group">
      <input type="text" class="form-control"
        placeholder="할 일을 입력하세요"
        v-model="context"
        v-on:keyup.enter="createTodo(context)"
      >
      <span class="input-group-btn">
        <button class="btn btn-default" type="button" @click="createTodo(context)">추가</button>
      </span>
    </div>
  </div>
</template>

<script>
  var output = [],
      value = [];
  localStorage.removeItem('loglevel:webpack-dev-server');
  for(var i = 0; i < localStorage.length; i++){
    output.push({context: localStorage.key(i)});
    var getVal = localStorage.getItem(localStorage.key(i));
    if(getVal === 'checked'){
      value.push(localStorage.key(i));
    }
  }

  export default {
    name: 'TodoPage',
    data() {
      return {
        context: null,
			  //todos: [],
        //todos: [{context: "output"}],
        todos: output,
        //checked: []
        checked: value,
        isChked: function(e){
          if(localStorage.getItem(e) === 'checked'){
            return true;
          } else {
            return false;
          }
        }
		  }
    },
    methods: {
      check: function(e){
        localStorage.removeItem('loglevel:webpack-dev-server');
        var id = e.target.id;
        console.log();
        if(this.checked.includes(id)){
          localStorage.setItem(id, 'checked');
          e.target.parentElement.classList.add('chked');
        } else {
          localStorage.setItem(id, 'unchecked');
          e.target.parentElement.classList.remove('chked');
        }
      },
      deleteTodo(context, i) {
        localStorage.removeItem(context);
        this.todos.splice(i, 1)
      },
      createTodo(context) {
        if(context != null){
          this.todos.push({context: context})
          localStorage.setItem(this.context, 'unchecked');
          this.context = null
        }
        localStorage.removeItem('loglevel:webpack-dev-server');
      }
    }
  }
</script>

<style>
  .container {
    display:flex;
    flex-direction:column;
    flex-wrap:wrap;
    margin:0 auto;
    padding:0;
    max-width:768px;
    height:100%;
    border:1px solid #eee;
    border-radius:4px;
  }
  h2 {flex:none; margin:0; padding:20px 15px; border-bottom:1px solid #eee;}
  .list-group {flex:1; overflow:auto; margin:0; padding:0; list-style:none;}
  .list-group-item {position:relative; padding:15px; border-bottom:1px solid #ddd;}
  .list-group-item input[type=checkbox] {position:absolute; top:50%; left:15px; margin:0; width:20px; height:20px; transform:translateY(-50%);}
  .list-group-item label {display:block; padding:0 30px;}
  .list-group-item.chked label {text-decoration:line-through; opacity:0.5;} 
  .btn-del {position:absolute; top:50%; right:15px; width:20px; height:20px; text-indent:-9999px; background:transparent; border:none; opacity:0.5; overflow:hidden; transform:translateY(-50%); transition:opacity .5s;}
  .btn-del:hover {opacity:1;}
  .btn-del:before, .btn-del:after {content:''; display:block; position:absolute; top:50%; left:50%; width:2px; height:20px; background:#f00; transform-origin:center;}
  .btn-del:before {transform:translate(-50%, -50%) rotate(45deg);}
  .btn-del:after {transform:translate(-50%, -50%) rotate(-45deg);}
  .input-group {flex:none; padding:10px; width:100%; background:#efefef; border-radius:0 0 4px 4px;}
  .form-control {padding:5px; width:calc(100% - 80px); line-height:2; border:1px solid #ddd;}
  .btn {padding:5px; width:74px; font-weight:bold; line-height:2; background:#fefefe; border:1px solid #eee;}
</style>