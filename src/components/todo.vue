<template>
  <div class="shape">
    <h1 class="text-center my-4 text-secondary py-2">Todo App</h1>
    <div class="container my-5">
      <div class="row">
        <div v-if="editing" class="d-flex justify-content-center">
          <input
            class="form-control text"
            type="text"
            v-model="todo"
            name="todo"
          />
          <button @click="UpdateTask()" class="btn btn-success ms-3">
            Update
          </button>
        </div>
        <div v-else class="d-flex justify-content-center">
          <input
            class="form-control text"
            type="text"
            v-model="todo"
            name="todo"
            
          />
          <button @click="addTask()" class="btn btn-success ms-3">
            AddTask
          </button>
        </div>
      </div>
    </div>

    <div class="container content">
      <div v-for="item in list" :key="item.id">
        <div class="card my-2  mx-auto">
          <div class="card-body d-flex justify-content-between align-items-center">
            <h4 class="">{{ item.todo }}</h4>
            <span>
              <button @click="EditTask(item.id,index)" class="btn btn-primary me-3">Edit</button>
              <button @click="DeleteTask(item.id)" class="btn btn-danger">Delete</button>
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo",
  data() {
    return {
      todo: "",
      editing: false,
      list: [],
      selected:null
    };
  },
  methods: {
    addTask() {
      if (this.todo == "") {
        alert("please enter a new task");
      } else {
        const newTodo = {
          id: new Date().getTime().toString(),
          todo: this.todo,
        };
        this.list.push(newTodo);
        this.todo = "";
      }
    },
    EditTask(id) {
      this.editing = true;
      const newTodo = this.list.filter((item) => item.id == id);
      this.todo = newTodo[0].todo;
      this.selected = this.list.indexOf(newTodo[0]);
      console.log(this.selected);
    },
    DeleteTask(id) {
      const newTodo = this.list.filter((item) => item.id != id);
      this.list = newTodo;
      this.editing = false;
    },
    UpdateTask() {
      this.list[this.selected].todo = this.todo;
      this.todo = "";
      this.editing = false;
    },
  },
};
</script>

<style>
  .shape{
    padding: 10px;
    border-radius: 10px;
    box-shadow: 0 0 10px #121212;
    margin: auto;
    
  }
  .content{
    max-height: 200px;
    overflow-y: scroll;
    scrollbar-width: none;
  }
  @media only screen and (min-width: 900px) {
  .shape {
    width: 40%;
  }
}
  @media only screen and (max-width: 900px) and (min-width: 500px) {
    .shape {
      width: 70%;
    }
    
  }
  @media only screen and (max-width: 500px) and (min-width: 300px) {
    .shape {
      width: 80%;
    }
    
  }
</style>
