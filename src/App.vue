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
  background-color: #6279c5;
}
.md-card {
  max-width: 900px;
  margin: auto;
  color: rgba(10, 67, 94, 0.651);
  background: #ffffff;
  font-weight: 500;
}
.header {
  text-align: center;
  background: linear-gradient(to bottom, #6279c5, #ffffff) !important;
  height: 130px;
}

.md-title {
  font-size: 3rem !important;
  color: rgba(10, 67, 94, 0.651);
  font-weight: bold;
  padding: 30px;
}

.taskadd {
  font-size: 1.5rem !important;
  color: rgba(10, 67, 94, 0.651);
  font-weight: 500;
}
.md-card-content {
  margin-right: 100px;
  margin-left: 100px;
  font-size: 1.5rem !important;
  background-color: #ffffff;
}

.md-field {
  min-width: 300px !important;
  max-width: 500px;
  border-bottom: 1px dotted rgba(10, 67, 94, 0.651);
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
  border-bottom: 1px dotted rgba(10, 67, 94, 0.651);
}

.edit {
  color: rgba(10, 67, 94, 0.651);
}
.todo-item-label {
  margin-left: 30px;
}
.is-complete {
  text-decoration: line-through;
  color: rgba(10, 67, 94, 0.651);
}
.btn-edit {
  color: rgba(10, 67, 94, 0.651);
}
.btn-delete {
  color: rgba(10, 67, 94, 0.651);
}
.completed {
  transform: scale(1.5);
}
</style>
