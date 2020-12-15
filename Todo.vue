<template>
  <div>
    <section class="">
      <div id="wrapper" class="">
        <div class="form-container">
          <header class="">
            <img src="./teflon.jpg" alt="" />
            <h1>TEFLON</h1>
          </header>
          <div class="">
            <p>{{ message }}</p>
            <ul id="list-todo">
              <li
                v-bind:class="{ 'line-through': todos.done }"
                v-for="(todos, index) in todos"
                v-bind:key="index"
              >
                <input type="checkbox" v-model="todos.done" v-on:change="checkbox" />
                {{ todos.title }}
              </li>
            </ul>
          </div>
          <div class="btn-container">
            <form action="#">
              <div class="input-text">
                <input type="text" v-model="addTodoText" />
              </div>
              <div v-if="error" class="error">Insert Todo</div>
              <button id="btn-add-todo" type="submit" class="" v-on:click="btnAddTodo">
                Lägg till Todo
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        { title: "Bananer", done: false },
        { title: "Kaffe", done: false },
        { title: "Keso", done: false },
        { title: "Rolig keps med djurmotiv", done: false },
      ],
      message: "",
      addTodoText: "",
      error: false,
    };
  },
  methods: {
    checkbox() {
      let result = this.todos.filter((todo) => (todo = todo.done == false));
      if (result.length == 0) this.message = "Du har gjort alla todos";
      else this.message = `Du har ${result.length} kvar att göra`;
      localStorage.Todo = this.message;
    },
    btnAddTodo() {
      let todoTemp = { title: this.addTodoText, done: false };
      if (this.addTodoText.length < 1) {
        this.error = true;
      } else {
        this.error = false;
        this.todos.push(todoTemp);
      }
      this.addTodoText = "";
      this.checkbox();
    },
    localStorage() {
      if (localStorage.Todo != null) {
        this.checkbox();
        this.message = localStorage.Todo;
      }
    },
  },
  created: function () {
    this.localStorage();
  },
};
</script>

<style>
section {
  display: flex;
  justify-content: center;
}
#wrapper {
  width: 400px;
  margin-top: 100px;
  padding: 50px;
  background-color: rgb(255, 255, 255);
  display: flex;
  justify-content: center;
  -webkit-box-shadow: 5px 5px 15px -3px #000000;
  box-shadow: 5px 5px 15px -3px #000000;
}
.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  -webkit-box-shadow: 5px 5px 15px -3px #000000;
  box-shadow: 5px 5px 15px -3px #000000;
  padding-bottom: 30px;
}

p {
  text-align: center;
  font-weight: bold;
  margin-top: 50px;
}

h1 {
  margin: 0px;
}

img {
  width: 100px;
  height: 80px;
}

ul {
  padding-inline-start: 0px;
}

li {
  list-style-type: none;
  margin: 10px;
  background-color: rgba(128, 128, 128, 0.507);
  width: 300px;
  height: 50px;
  padding-left: 20px;
  display: flex;
  align-items: center;
}

ul li {
  text-decoration: none;
  transition: background-color0.2s;
}

ul li:hover {
  background-color: #95b7cf;
}

input[type="checkbox"] {
  margin-right: 10px;
  transform: scale(1.8);
}

input[type="checkbox"]:hover {
  box-shadow: 0px 0px 5px #0075ff;
  cursor: pointer;
}

.error {
  color: red;
  text-align: center;
}

.input-text {
  padding: 10px;
  margin-left: 4px;
  border-width: 1px;
  border-color: #cccccc;
  background-color: #ffffff;
  color: #000000;
  border-style: solid;
  border-radius: 5px;
  box-shadow: 0px 0px 5px rgba(66, 66, 66, 0.75);
  display: flex;
  justify-content: center;
  width: 275px;
}
.input-text:hover {
  background-color: #95b7cf;
}

.input-text input {
  font-size: 20px;
  border: 2px solid white;
  background-color: rgba(243, 243, 243, 0.513);
}

button {
  margin: 3px;
  width: 250px;
  height: 50px;
  border-radius: 10px;
  width: 300px;
  display: flex;
  align-items: center;
  justify-content: center;
}

button:hover {
  background-color: #95b7cf !important;
}

button:first-child {
  background-color: rgb(255, 255, 255);
}

button:last-child {
  background-color: rgb(20, 20, 20);
  color: white;
}
.line-through {
  text-decoration: line-through;
}
</style>
