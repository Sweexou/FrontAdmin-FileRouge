<script lang="ts">
  import LoginPage from './pages/LoginPage.svelte';
  import TablePage from './pages/TablePage.svelte';
  import QuestionnaireTable from './pages/QuestionnaireTable.svelte';
  import UserDetail from './pages/UserDetail.svelte';
  import Stats from './pages/Stats.svelte';

  type User = {
    uuid: string;
    classement: number;
    name: string;
    creation: string;
    score: number;
    username?: string;
    email?: string;
    lastConnection?: string;
  };

  let isLoggedIn: boolean = false;
  let currentPage: 'users' | 'questionnaires' | 'userDetail' | 'stats' = 'users';
  let selectedUser: User | null = null;

  function handleLogin(): void {
    isLoggedIn = true;
  }

  function setCurrentPage(page: 'users' | 'questionnaires' | 'userDetail' | 'stats'): void {
    currentPage = page;
  }

  // Correction : accepter User | null
  function setSelectedUser(user: User | null): void {
    selectedUser = user;
  }
</script>

{#if isLoggedIn}
  {#if currentPage === 'users'}
    <TablePage {setCurrentPage} {setSelectedUser} />
  {:else if currentPage === 'questionnaires'}
    <QuestionnaireTable {setCurrentPage} {setSelectedUser} />
  {:else if currentPage === 'userDetail'}
    <UserDetail {setCurrentPage} {selectedUser} {setSelectedUser} />
  {:else if currentPage === 'stats'}
    <Stats {setCurrentPage} />
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
