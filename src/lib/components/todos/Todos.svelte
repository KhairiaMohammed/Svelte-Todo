<script>
  import Todo from "./Todo.svelte";

  export let todos = []
  export let activeEditTodo;

  $: activeTodos = activeEditTodo ? [activeEditTodo] : todos

</script>

<div class="todos-list">
  {#each activeTodos as todo (todo.id) }
    
  <Todo  {todo} {activeEditTodo} on:deleteTodo on:editTodo on:toggleTodo/>
  {/each}

  {#if todos.length === 0}
    <h3 class="no-todos"> لا يوجد مهام حالية ... </h3>
  {/if}
  
</div>

