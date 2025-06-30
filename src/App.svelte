<script lang="ts">
  import LoginPage from './pages/LoginPage.svelte';
  import TablePage from './pages/TablePage.svelte';
  import QuestionnaireTable from './pages/QuestionnaireTable.svelte';

  let isLoggedIn: boolean = false;
  let currentPage: 'users' | 'questionnaires' = 'users';

  function handleLogin(): void {
    isLoggedIn = true;
  }

  function setCurrentPage(page: 'users' | 'questionnaires'): void {
    currentPage = page;
  }
</script>

{#if isLoggedIn}
  {#if currentPage === 'users'}
    <TablePage {setCurrentPage} />
  {:else if currentPage === 'questionnaires'}
    <QuestionnaireTable {setCurrentPage} />
  {/if}
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
