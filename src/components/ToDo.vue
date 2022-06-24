<template>
  <div class="container shadow-lg px-5 py-5 rounded-3">
    <h1 class="mb-5">Список дел</h1>

    <!-- <form> -->
    <div class="d-flex mb-5">
      <input
        v-model="newTodo"
        type="text"
        placeholder="Добавить задачу"
        class="form-control form-input me-3"
      />
      <button type="submit" class="submit-btn px-3 py-2" @click="addTodo()">
        +
      </button>
    </div>
    <!-- </form> -->

    <div
      class="row todo-list shadow px-3 pt-3 pb-2 align-items-center mb-4"
      v-for="(todo, index) in todos"
      :key="index"
    >
      <div class="col-7 text-start">
        <h5 :class="{ 'todo-Сделано': todo.status === 'Сделано' }">
          {{ todo.name }}
        </h5>
      </div>
      <div class="col-2">
        <div class="d-flex justify-content-start align-items-center">
          <div
            class="status-indicator mb-1 me-2"
            :class="{
              'status-indicator-todo': todo.status === 'Сделать',
              'status-indicator-Делается': todo.status === 'Делается',
              'status-indicator-Сделано': todo.status === 'Сделано',
            }"
          ></div>
          <div
            class="status-text"
            @click="changeStatus(index)"
            :class="{
              'status-text-todo': todo.status === 'Сделать',
              'status-text-Делается': todo.status === 'Делается',
              'status-text-Сделано': todo.status === 'Сделано',
            }"
          >
            <h5>{{ todo.status }}</h5>
          </div>
        </div>
      </div>
      <div class="col-3 text-end action-btn">
        <div class="d-flex justify-content-end">
          <div class="" @click="upTodo(index)">
            <i class="uil uil-arrow-up ms-4"></i>
          </div>
          <div class="" @click="downTodo(index)">
            <i class="uil uil-arrow-down ms-4"></i>
          </div>
          <div class="" @click="editTodo(index)">
            <i class="uil uil-edit-alt ms-4"></i>
          </div>
          <div class="" @click="deleteTodo(index)">
            <i class="uil uil-trash-alt ms-4"></i>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ToDo",

  data() {
    return {
      newTodo: "",
      indexEditTodo: null,
      tempNameTodo: "",
      tempStatusTodo: "",
      todoStatus: ["Сделать", "Делается", "Сделано"],
      todos: [
        {
          name: "Поехать за смузи",
          status: "Сделать",
        },
        {
          name: "Поесть мусса",
          status: "Сделано",
        },
        {
          name: "Пососать",
          status: "Делается",
        },
      ],
    };
  },

  methods: {
    addTodo() {
      if (this.newTodo.length === 0) return;

      if (this.indexEditTodo === null) {
        this.todos.push({
          name: this.newTodo,
          status: "Сделать",
        });
      } else {
        this.todos[this.indexEditTodo].name = this.newTodo;
        this.indexEditTodo = null;
      }

      this.newTodo = "";
    },
    editTodo(index) {
      this.newTodo = this.todos[index].name;
      this.indexEditTodo = index;
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
    changeStatus(index) {
      let statusIndex = this.todoStatus.indexOf(this.todos[index].status);

      if (++statusIndex > 2) statusIndex = 0;
      this.todos[index].status = this.todoStatus[statusIndex];
    },
    upTodo(index) {
      if (index === 0) return;

      this.tempNameTodo = this.todos[index].name;
      this.tempStatusTodo = this.todos[index].status;

      this.todos[index].name = this.todos[index - 1].name;
      this.todos[index].status = this.todos[index - 1].status;

      this.todos[index - 1].name = this.tempNameTodo;
      this.todos[index - 1].status = this.tempStatusTodo;
    },
    downTodo(index) {
      if (index === this.todos.length - 1) return;

      this.tempNameTodo = this.todos[index].name;
      this.tempStatusTodo = this.todos[index].status;

      this.todos[index].name = this.todos[index + 1].name;
      this.todos[index].status = this.todos[index + 1].status;

      this.todos[index + 1].name = this.tempNameTodo;
      this.todos[index + 1].status = this.tempStatusTodo;
    },
  },
};
</script>

<style scoped>
.form-input {
  border: 1px solid #333;
  border-radius: 50px;
}
.form-control:focus {
  box-shadow: none;
  /* border: none; */
}
.submit-btn {
  background-color: skyblue;
  border-radius: 50%;
  border: none;

  font-size: 20px;
  font-weight: 800;
  color: #333;
}
.todo-list {
  border-radius: 50px;
}
.todo-Сделано {
  font-style: italic;
  text-decoration: line-through;
}
.status-indicator {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}
.status-indicator-todo {
  background: red;
}
.status-indicator-Делается {
  background: yellow;
}
.status-indicator-Сделано {
  background: green;
}
.status-text {
  font-weight: bold;
  cursor: pointer;
}
.status-text-todo {
  color: red;
}
.status-text-Делается {
  color: yellow;
}
.status-text-Сделано {
  color: green;
}
.action-btn i {
  font-size: 25px;
  cursor: pointer;
}
</style>
<style>
body {

  background-image:
      linear-gradient(90deg, rgba(7, 86, 160, 0.937) 1%, rgba(255, 122, 151, 0.5) 15%),
      linear-gradient(44deg, rgba(0, 43, 99, 0.079) 39%, rgba(242, 140, 143, 0.5) 18%),
      linear-gradient(118deg, rgba(84, 202, 242, 0.031) 40%, rgba(247, 155, 187, 0.5) 54%),
      linear-gradient(58deg, rgba(90, 90, 237, 0.161) 83%, rgba(249, 156, 142, 0.5) 23%);
  background-blend-mode: normal, lighten, multiply, hard-light;
  font-family: "Times New Roman",serif;
  overflow: hidden;
}
</style>
