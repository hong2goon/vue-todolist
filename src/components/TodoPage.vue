<template>
  <div class="container">
    <h2>Todo List</h2>
    
    <ul class="list-group">
      <li class="list-group-item" v-for="(todo, index) in todos">
        <span>{{ todo.context }}</span>
        <button type="button" class="btn-del" @click="deleteTodo(index)">삭제</button>
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
  export default {
    name: 'TodoPage',
    data() {
      return {
        context:null,
			  todos: [{context:'청소'},{context:'블로그 쓰기'},{context:'밥먹기'},{context:'안녕'}]
		  }
    },
    methods: {
      deleteTodo(i) {
        this.todos.splice(i, 1)
      },
      createTodo(context) {
        if(context != null){
          this.todos.push({context: context})
          this.context = null
        }
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
  .btn-del {position:absolute; top:50%; right:15px; width:20px; height:20px; text-indent:-9999px; background:transparent; border:none; opacity:0.5; overflow:hidden; transform:translateY(-50%); transition:opacity .5s;}
  .btn-del:hover {opacity:1;}
  .btn-del:before, .btn-del:after {content:''; display:block; position:absolute; top:50%; left:50%; width:2px; height:20px; background:#f00; transform-origin:center;}
  .btn-del:before {transform:translate(-50%, -50%) rotate(45deg);}
  .btn-del:after {transform:translate(-50%, -50%) rotate(-45deg);}
  .input-group {flex:none; padding:10px; width:100%; background:#efefef; border-radius:0 0 4px 4px;}
  .form-control {padding:5px; width:calc(100% - 80px); line-height:2; border:1px solid #ddd;}
  .btn {padding:5px; width:74px; font-weight:bold; line-height:2; background:#fefefe; border:1px solid #eee;}
</style>