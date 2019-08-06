<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div>
      <button @click="addTodo">ADD TASK</button>
      <button @click="removeTodo">DELTETE FINISHED TASKS</button>
    </div>
    <p>input: <input v-model="newTodo" placeholder="test"></p>
    <div class="task-list">
      <div v-for="todo in todos" 
        :key="todo.id">
        <input type="checkbox"
          @change="toggle(todo)"
          :checked="todo.done">
        <span @click="editTodo(todo)">  
        <del v-if="todo.done">
          {{ todo.text }}
        </del>
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
        {id: 0, text: '0', done: false, edit:false},
        {id: 1, text: '1', done: false, edit:false},
        {id: 2, text: '2', done: false, edit:false},
        {id: 3, text: '3', done: false, edit:false},
        {id: 4, text: '4', done: true, edit:false},
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
console.log(todo.edit)
        //選択を外したら（画面の他の部分をタップしたら）editをfalseにしたい。
       todo.edit = !todo.edit
     }
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
  align-items: center;
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
</style>
