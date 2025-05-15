<script>
  import {CircleIcon } from 'svelte-feather-icons'
  import { createEventDispatcher} from 'svelte'
  const dispatch = createEventDispatcher()

  export let activeEditTodo;
  export let isFilter

  let value = ''

  const handleAddTodo = () => {
    if(!value.trim() ) {
      return
    }
    dispatch('addTodo' , value.trim())
    value = ''
  }

  const editChange = () => {
    if(activeEditTodo){
      value = activeEditTodo.title
    }
  }

  const handleFilter = () => {
    dispatch('filter'  )
  }

  $: activeEditTodo, editChange()

</script>

<div class="todos-form">
  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <!-- svelte-ignore a11y_no_static_element_interactions -->
  <div class="todos-form_icon" class:active={isFilter} on:click={handleFilter}>
    <CircleIcon />
  </div>
   
  <div class="todos-form_form">
    <input bind:value  type="text" placeholder="اضف مهمة جديدة ..." />
  </div>
  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <!-- svelte-ignore a11y_no_static_element_interactions -->
  <div class="todos-form_submit" on:click={handleAddTodo}>
    <button class="btn" disabled={!value.trim()}> 
      {
        activeEditTodo ? 
        'تعديل' :
        'اضافة'
      }
      
        </button>
  </div>
</div>

