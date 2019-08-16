<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>input: <input v-model="newTodo" placeholder="test" @keypress="applyTodo" class="addText"></p>
    <div>
      <div class="btn-class"
        @click="addTodo"><p class="btn-name">追加</p></div>
      <div class="btn-class"
        @click="removeTodo"><p class="btn-name">削除</p></div>
    </div>
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
          <input 
            v-model="todo.text" 
            v-else-if="todo.edit" 
            class="task-text">
          <span v-else>
            {{ todo.text }}
          </span>
        </span>
      </div>
    </div>
    <!-- <pre>{{ $data }}</pre> -->
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
        {id: 4, text: '4', done: true, edit:false}
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
     applyTodo: function(keyCode) {
       //console.log(keyCode.charCode)
        if(keyCode.charCode === 13) {
          this.addTodo()
        }
     }
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
  padding-top:1rem;
  padding-bottom:10rem;
  padding-left:38vw;
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
  font-size: 1rem;
}
.task {
  text-align: left;   
}
.btn-class {
    width: 10%;
    border-radius: 5px;
    background: #a2bfda;
    display: inline-block;
    height: 30px;
    -webkit-transition: all 0.3s ease;
    -moz-transition: all 0.3s ease;
    -o-transition: all 0.3s ease;
    transition: all  0.3s ease;
}
.btn-class:hover {
    background: #ffc9d7;
}
.btn-class p {
  line-height: 30px;
  margin: 0;
}
.addText {
  height: 1.5rem;
  border: 0px solid #000000;
  border-bottom: 2px solid #555555;
}
.addText:hover {
  background-color: #908bdd80;
}
</style>
