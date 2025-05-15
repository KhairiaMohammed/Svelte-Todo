<script>
  import { onMount } from "svelte";

  let theme = false; // false = light, true = dark

  onMount(() => {
    const storedTheme = localStorage.getItem("theme");
    theme = storedTheme === "dark";
    updateBodyClass();
  });

  function toggleTheme() {
    theme = !theme;
    localStorage.setItem("theme", theme ? "dark" : "light");
    updateBodyClass();
  }

  function updateBodyClass() {
    if (typeof document !== "undefined") {
      document.body.classList.toggle("dark", theme);
      document.body.classList.toggle("light", !theme);
    }
  }
</script>

<div>
  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <nav class="navbar" class:light={!theme} class:dark={theme}>
    <a class="link" class:light={!theme} class:dark={theme} href="/">الرئيسية</a
    >
    <!-- <a class="link" class:light={!theme} class:dark={theme} href="/الب"
      >Page One</a
    >
    <a class="link" class:light={!theme} class:dark={theme} href="/pageTwo"
      >Page Two</a
    >
    <a class="link" class:light={!theme} class:dark={theme} href="/pageThree"
      >Page Three</a
    > -->
    <!-- svelte-ignore a11y_no_static_element_interactions -->
    <div
      on:click={toggleTheme}
      class:light-icon={!theme}
      class:dark-icon={theme}
      style="cursor: pointer; font-size: 1.5rem;"
      aria-label="Toggle theme"
    >
      {#if theme}
        ☀️
      {:else}
        🌙
      {/if}
    </div>
  </nav>
</div>

<!-- <style>

</style> -->
