<script>
  import Header from "../lib/components/layout/Header.svelte";
  import Todos from '../lib/components/todos/Todos.svelte'
  import TodosForm from "../lib/components/todos/TodosForm.svelte";

let todos = [
  { id: 1, title: "شراء مستلزمات", done: false },
  { id: 2, title: "شراء منتجات", done: true },
  { id: 3, title: "مشاهدة الكورس", done: false },
  { id: 4, title: "كتابة الكود", done: true },
];

let isFilter = false
let activeEditTodo = null

const addTodo = (e) => {
  const title = e.detail
  const id = new Date().getTime()
  if(!activeEditTodo) {

    todos = [ {
      title , id , done: false
    } , ...todos]
  } else {
    // edit mode 
    todos = todos.map(t => {
      if(activeEditTodo.id === t.id) {
        t.title = title
      }
      return t
    })
    activeEditTodo = null
  }
   
}

const deleteTodo = (e) => {
  const id = e.detail
  todos = todos.filter(t =>t.id !== id)
}

const editTodo = (e) => {
  activeEditTodo = e.detail
}

const toggleTodo = (e) => {
  if(activeEditTodo) {
    return
  }
  const id = e.detail
  todos = todos.map(t =>{
    if(t.id === id) {
      t.done = !t.done
    }
    return t
   })
}

const filter = () => {
  isFilter = !isFilter
}

$: allTodos = isFilter ? todos.filter(t => !t.done) : todos

</script>

<main>
  <div class="container">
    <div class="todos">
      <TodosForm {activeEditTodo} {isFilter} on:addTodo={addTodo} on:filter={filter} />
      <Todos  todos={allTodos} {activeEditTodo} on:deleteTodo={deleteTodo} on:editTodo={editTodo} on:toggleTodo={toggleTodo} />
    </div>
  </div>
</main>