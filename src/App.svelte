<script lang="ts">
  import LoginPage from './pages/LoginPage.svelte';
  import TablePage from './pages/TablePage.svelte';

  let isLoggedIn = false;

  function handleLogin() {
    isLoggedIn = true;
  }
</script>

{#if isLoggedIn}
  <TablePage />
{:else}
  <LoginPage onLogin={handleLogin} />
{/if}

<style>
  :global(html, body) {
    height: 100%;
    width: 100%;
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
  }

  :global(#app) {
    flex: 1;
    display: flex;
    flex-direction: column;
    width: 100%;
  }
</style>
