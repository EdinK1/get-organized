<template>
  <main>
    <nav class="tabs">
      <p
        class="tab"
        v-for="(tab, index) in tabs"
        :key="index"
        @click="selectedTab = tab"
        :class="{ activeTab: selectedTab === tab }"
      >
        {{ tab }}
      </p>
    </nav>

    <draggable
      v-show="selectedTab === 'All'"
      class="todos"
      tag="ul"
      v-model="todos"
      v-bind="dragOptions"
      @start="isDragging = true"
      @end="isDragging = false"
    >
      <transition-group type="transition" name="flip-list">
        <li class="todo" v-for="todo in todos" :key="todo.id">
          <h3 class="todo-title">{{ todo.title }}</h3>
          <p class="todo-desc">{{ todo.desc }}</p>
          <button class="delete-button" @click="deleteTodo(todo.id)">
            Delete
          </button>
          <button class="completed-button" @click="completeTodo(todo.id)">
            Mark as done
          </button>
        </li>
      </transition-group>
    </draggable>

    <draggable
      v-show="selectedTab === 'Done'"
      class="todos"
      tag="ul"
      v-model="todos"
      v-bind="dragOptions"
      @start="isDragging = true"
      @end="isDragging = false"
    >
      <transition-group type="transition" name="flip-list">
        <li class="todo" v-for="todo in completedTodos" :key="todo.id">
          <h3 class="todo-title">{{ todo.title }}</h3>
          <p class="todo-desc">{{ todo.desc }}</p>
          <button class="delete-button" @click="deleteTodo(todo.id)">
            Delete
          </button>
          <button class="completed-button" @click="inCompleteTodo(todo.id)">
            Unmark from done
          </button>
        </li>
      </transition-group>
    </draggable>
    <p class="done" v-if="todos.length === 0">All done! 🎉</p>
    <p
      class="done"
      v-show="completedTodos.length == 0 && selectedTab === 'Done'"
    >
      Nothing here 🌵
    </p>
  </main>
</template>

<script>
import draggable from 'vuedraggable'

export default {
  components: {
    draggable
  },
  data() {
    return {
      tabs: ['All', 'Done'],
      selectedTab: 'All',
      todos: [
        {
          id: 1,
          title: 'Clean up room',
          desc: 'clean up your room, you lazy potato 🥔'
        },
        {
          id: 2,
          title: 'Brush teeth',
          desc: 'Teeth are very important 😁'
        },
        {
          id: 3,
          title: 'Do groceries',
          desc: "Don't forget the avocados, pls 🥑"
        }
      ],
      completedTodos: []
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    completeTodo(id) {
      const completedTodo = this.todos.find(todo => todo.id === id)
      this.completedTodos.push(completedTodo)
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    inCompleteTodo(id) {
      const todo = this.completedTodos.find(todo => todo.id === id)
      this.todos.push(todo)
      this.completedTodos = this.completedTodos.filter(todo => todo.id !== id)
    },
    noResults() {
      if (this.selectedTab === 'Done') {
        return true
      }
    }
  },
  computed: {
    dragOptions() {
      return {
        animation: 0,
        group: 'description',
        disabled: false,
        ghostClass: 'ghost'
      }
    }
  }
}
</script>

<style scoped>
.tabs {
  display: flex;
  justify-content: center;
  padding-top: 3rem;
}

.tab {
  font-size: 1.25rem;
  padding: 0 1.5rem;
  font-weight: 100;
  cursor: pointer;
}

.activeTab {
  font-weight: 400;
}
.todos {
  list-style: none;
  max-width: 600px;
  width: 90%;
  margin: 0 auto;
  padding: 1rem;
}

.todo {
  position: relative;
  margin: 1rem 0;
  padding: 1rem;
  box-shadow: 0px 0px 5px 0px rgba(0, 0, 0, 0.3);
  text-align: left;
  cursor: pointer;
}

.todo-list {
  font-size: 1.25rem;
}

.todo-desc {
  font-style: italic;
  font-weight: 100;
}

.delete-button,
.completed-button {
  background-color: #b33a3a;
  border: none;
  color: #fff;
  padding: 0.5rem 1.5rem;
  font-size: 1.05rem;
  transition: background 0.4s ease-in-out;
  cursor: pointer;
}

.completed-button {
  margin-left: 1rem;
  background: #3a64b3;
}

.delete-button:hover {
  background-color: #ee1e1e;
}

.completed-button:hover {
  background-color: #5e8bdd;
}

.done {
  padding: 3rem 0;
  font-size: 1.75rem;
}

.flip-list-move {
  transition: transform 0.5s;
}
.no-move {
  transition: transform 0s;
}

.ghost {
  background-color: rgb(248, 248, 237);
}
</style>
