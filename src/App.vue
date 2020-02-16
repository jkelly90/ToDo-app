<template>
  <div class="container">
    <md-card>
      <md-card-header class="header">
        <div class="md-title">To do...</div>
      </md-card-header>
      <md-card-content>
        <md-field>
          <md-input
            class="taskadd"
            v-model="currentTodo"
            @keydown.enter="addTodo()"
            placeholder="add task"
          ></md-input>
        </md-field>
        <div class="todo-list">
          <ul class="todos">
            <li class="todo-item" v-for="todo in todos" :key="todo.id">
              <span>
                <input
                  class="completed"
                  type="checkbox"
                  @change="toggleCompleted"
                  v-model="todo.completed"
                />
                <span
                  v-if="todo.editing === false"
                  class="todo-item-label"
                  :class="{'is-complete': todo.completed}"
                  @dblclick="editTodo(todo)"
                >{{ todo.label}}</span>

                <div v-if="todo.editing">
                  <md-field>
                    <md-input
                      class="edit"
                      type="text"
                      v-model="todo.label"
                      @keyup.enter="stopEdit(todo)"
                      @keyup.esc="stopEdit(todo)"
                      @focusout="stopEdit(todo)"
                      placeholder="edit"
                    ></md-input>
                  </md-field>
                </div>
              </span>

              <span class="actions">
                <md-button class="btn-edit" @click="editTodo(todo)">
                  <md-icon>edit</md-icon>
                </md-button>

                <md-button class="btn-delete" @click="removeTodo(todo)">
                  <md-icon>delete</md-icon>
                </md-button>
              </span>
            </li>
          </ul>
        </div>
      </md-card-content>
    </md-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      editedTodo: ""
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: false,
        editing: false
      });
      this.currentTodo = "";
    },

    toggleCompleted() {
      this.todo.completed = !this.todo.completed;
    },

    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },

    editTodo(todo) {
      todo.editing = true;
    },

    stopEdit(todo) {
      todo.editing = false;
    }
  }
};
</script>

<style>
body {
  background-color: #80acca;
}
.md-card {
  max-width: auto;
  margin: auto;
  color: #4244c4f3;
  background: #80acca;
}
.header {
  text-align: center;
  background: linear-gradient(
    to bottom,
    rgba(0, 84, 240, 0.781),
    #80acca
  ) !important;
  color: white !important;
  font-weight: bold;
}

.md-title {
  font-size: 3rem !important;
  color: white;
  font-weight: bold;
}

.taskadd {
  font-size: 1.5rem !important;
  color: white;
}
.md-card-content {
  margin-right: 100px;
  margin-left: 100px;
  font-size: 1.5rem !important;
  color: white;
}

.md-field {
  min-width: 400px !important;
  max-width: 400px;
  border-bottom: 1px solid white;
  font-size: 3em !important;
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
.todo-item {
  margin-top: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-bottom: 1px solid white;
}

.edit {
  color: white;
}
.todo-item-label {
  margin-left: 30px;
}
.is-complete {
  text-decoration: line-through;
  color: white;
}
.btn-edit {
  color: white;
}
.btn-delete {
  color: rgba(0, 84, 240, 0.781);
}
.completed {
  transform: scale(1.5);
}
</style>
