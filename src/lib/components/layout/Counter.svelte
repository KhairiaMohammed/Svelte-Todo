<script>
  import { error } from "@sveltejs/kit";
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  export let user;
  let count = 0;
  const increment = () => {
    count += 1;
    dispatch("changeName", "kokha");
  };
  let list = ["ali", "fofo"];
  const fetchTodo = async () => {
    const res = await fetch(
      "https://jsonplaceholder.typicode.com/todos?_limit=5"
    );
    const data = await res.json();
    if (res.ok) {
      list = data;
    } else {
      throw new Error("error in api");
    }
  };
</script>

<button on:click={increment}>
  count is {count}
  <p>{user}</p>
  {#await fetchTodo()}
    <p>Loading ..</p>
  {:then data}
    {#each list as name}
      <p>{name.title}</p>
    {/each}
  {:catch error}
    <p>{error}</p>
  {/await}
</button>
