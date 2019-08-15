<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>
      <button @click="addTodo">ADD TASK</button>
      <button @click="removeTodo">DELTETE FINISHED TASKS</button>
    </div>
    <p>input: <input v-model="newTodo" placeholder="test"></p>
    <input type="date"/>
    <div class="task-list">
      <div class="task"
        v-for="todo in todos" 
        :key="todo.id">
        <input type="checkbox"
          @change="toggle(todo)"
          :checked="todo.done">
        <span @click="editTodo(todo)">  
          <del v-if="todo.done">
            {{ todo.text }}
          </del>
          <input v-model="todo.text" v-else-if="todo.edit" class="task-text">
          <span v-else>
            {{ todo.text }}
          </span>
        </span>
      </div>
    </div>
    <pre>{{ $data }}</pre>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: '*',
      todos: [
        {id: 0, text: '0', done: false, edit:true},
        {id: 1, text: '1', done: false, edit:true},
        {id: 2, text: '2', done: false, edit:true},
        {id: 3, text: '3', done: false, edit:true},
        {id: 4, text: '4', done: true, edit:true},
      ],
      maxId: 5,
      newTodo: ""
    }
  },
  methods: {
    addTodo: function(event) {
      if(!this.newTodo) return

      this.todos.push({
        id:   this.maxId,
        text: this.newTodo,
        done: false,
        edit: false
      })
      this.maxId += 1
      this.newTodo = ''
    },
    toggle: function(todo) {
      todo.done = !todo.done
    },
    removeTodo: function(event) {
      for(let i = this.todos.length - 1; i >= 0; i--) {
        if(this.todos[i].done) this.todos.splice(i, 1)
       }
     },
     editTodo: function(todo) {
       if(todo.done) return
       //console.log(todo.edit)
       todo.edit = true
     },
    //  fixTodo: function() {
    //     this.todos.forEach(function (item) {
    //     console.log(item);
    // });
    //     fixTodo: function() {
    //     this.todos.map(function (obj) {
    //     console.log(obj.edit);
    //     obj.edit = false
    //   });
    //  }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
/*
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
*/
@mixin flex-vender() {
  display: flex;
  display: -webkit-flex;
  display: -moz-flex;
  display: -ms-flex;
  display: -o-flex;
}
.task-list {
  @include flex-vender;
  flex-direction: column;
  // align-items: center;
  padding: 0 20vw;
  &__item {
    width: 270px;
    text-align: left;
    $element: #{&};
    &--checked {
      @extend #{$element};
      color: #85a6c6;
    }
  }
}
pre {
  text-align: left;
}
.task-text {
  border: none;
}
.task {
  text-align: left;   
}
</style>
