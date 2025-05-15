<script>
  import {CircleIcon , CheckCircleIcon , EditIcon , Trash2Icon } from 'svelte-feather-icons'

  import { fly } from 'svelte/transition'
  import { createEventDispatcher} from 'svelte'
  const dispatch = createEventDispatcher()

  export let todo;
  export let activeEditTodo;

  const handleDelete = () => {
    dispatch('deleteTodo' , todo.id)
  }
  const handleEdit = () => {
    dispatch('editTodo' , todo )
  }

  const handleToggleTodo = () => {
    dispatch('toggleTodo' , todo.id   )
  }

</script>


<div class="todos-todo " class:done={todo.done} in:fly={{x: 100, duration: 400}} out:fly={{x: -100, duration: 400}}  >
  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <!-- svelte-ignore a11y_no_static_element_interactions -->
  <div class="todos-todo_icon" on:click={handleToggleTodo}>
    {#if todo.done}
      <CheckCircleIcon />
      {:else}

      <CircleIcon />
    {/if}
  </div>
  <div class="todos-todo_text"> {todo.title} </div>

  {#if !activeEditTodo}
  <div class="todos-todo_cta">
    <!-- svelte-ignore a11y_click_events_have_key_events -->
    <!-- svelte-ignore a11y_no_static_element_interactions -->
    <div class="todos-todo_cta-edit" on:click={handleEdit}> 
      <EditIcon size="20" />  
    </div>
    <!-- svelte-ignore a11y_click_events_have_key_events -->
    <!-- svelte-ignore a11y_no_static_element_interactions -->
    <div class="todos-todo_cta-delete" on:click={handleDelete}> 
      <Trash2Icon size="20" />  
    </div>
  </div>
  {/if}
</div>
