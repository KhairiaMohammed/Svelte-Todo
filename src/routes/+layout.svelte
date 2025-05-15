<script>
    import Navbar from "../lib/components/layout/Navbar.svelte";
    import "../app.css";
    let theme = false;
  
    if (typeof window !== 'undefined') {
      const savedTheme = localStorage.getItem('theme');
      theme = savedTheme === 'dark';
    }
  
    $: if (typeof localStorage !== 'undefined') {
      localStorage.setItem('theme', theme ? 'dark' : 'light');
    }
  </script>
  
  <Navbar bind:theme={theme} />

  <div class="app-container" class:light-theme={!theme} class:dark-theme={theme}>
    <slot />
  </div>
  
  <style>
    .app-container {
      min-height: 100vh;
      width: 100%;
      padding: 3rem;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
  
    .light-theme {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      font-size: 16;
      
    }
  
    .dark-theme {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      font-size: 16;
    }

    
  </style>
  