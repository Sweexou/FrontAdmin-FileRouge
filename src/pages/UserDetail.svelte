<script lang="ts">
  interface Props {
    setCurrentPage: (page: 'users' | 'questionnaires' | 'userDetail' | 'stats') => void;
    selectedUser: User | null;
    setSelectedUser: (user: User | null) => void;
  }

  let { setCurrentPage, selectedUser, setSelectedUser }: Props = $props();

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

  function goBackToUsers() {
    setSelectedUser(null);
    setCurrentPage('users');
  }

  function deleteUser() {
    if (selectedUser && confirm(`Êtes-vous sûr de vouloir supprimer l'utilisateur ${selectedUser.name} ?`)) {
      // Logique de suppression ici
      console.log('Suppression de l\'utilisateur:', selectedUser.uuid);
      goBackToUsers();
    }
  }

  function formatDate(dateString: string): string {
    return new Date(dateString).toLocaleDateString('fr-FR', {
      year: 'numeric',
      month: 'long',
      day: 'numeric'
    });
  }
</script>

<header>
  <nav>
    <button 
      type="button" 
      class="nav-item active" 
      onclick={() => setCurrentPage('users')}
    >
      Users
    </button>
    <button 
      type="button" 
      class="nav-item" 
      onclick={() => setCurrentPage('questionnaires')}
    >
      Questionnaires
    </button>
    <button 
      type="button" 
      class="nav-item" 
      onclick={() => setCurrentPage('stats')}
    >
      Stats
    </button>
  </nav>
</header>

<main>
  <div class="detail-container">
    <div class="detail-header">
      <button class="back-btn" onclick={goBackToUsers}>
        ← Retour aux utilisateurs
      </button>
      <h1>Détails de l'utilisateur</h1>
    </div>

    {#if selectedUser}
      <div class="user-card">
        <div class="user-info">
            <div class="info-row">
                <span class="label">UUID</span>
                <span class="uuid-text">{selectedUser.uuid}</span>
            </div>

            <div class="info-row">
                <span class="label">Classement</span>
                <span class="rank-badge">{selectedUser.classement}</span>
            </div>

            <div class="info-row">
                <span class="label">Nom d'utilisateur</span>
                <span class="value">{selectedUser.username || selectedUser.name}</span>
            </div>

            <div class="info-row">
                <span class="label">Email</span>
                <span class="value">{selectedUser.email || 'Non renseigné'}</span>
            </div>

            <div class="info-row">
                <span class="label">Date de création</span>
                <span class="date-value">{formatDate(selectedUser.creation)}</span>
            </div>

            <div class="info-row">
                <span class="label">Score</span>
                <span class="score-badge">{selectedUser.score}</span>
            </div>

            <div class="info-row">
                <span class="label">Date de dernière connexion</span>
                <span class="date-value">{selectedUser.lastConnection ? formatDate(selectedUser.lastConnection) : 'Jamais connecté'}</span>
            </div>
            </div>


        <div class="actions">
          <button class="delete-btn" onclick={deleteUser}>
            🗑️ Supprimer l'utilisateur
          </button>
        </div>
      </div>
    {:else}
      <div class="error-message">
        <p>Aucun utilisateur sélectionné</p>
        <button class="back-btn" onclick={goBackToUsers}>
          Retour aux utilisateurs
        </button>
      </div>
    {/if}
  </div>
</main>

<style>
  :global(html, body, #app) {
    height: 100vh;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    background: #f5f8fa;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  }

  header {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 64px;
    background: #fff;
    box-shadow: 0 2px 8px rgba(33,84,162,0.04);
    z-index: 100;
  }

  nav {
    display: flex;
    align-items: center;
    height: 100%;
    padding: 0 1rem;
    gap: 2rem;
  }

  .nav-item {
    color: #2154a2;
    font-weight: 600;
    padding: 0.5rem 1rem;
    border-bottom: 2.5px solid transparent;
    cursor: pointer;
    transition: all 0.2s;
    white-space: nowrap;
    background: none;
    border: none;
    border-bottom: 2.5px solid transparent;
    font-size: 1.1rem;
    font-family: inherit;
    height: 100%;
    display: flex;
    align-items: center;
  }

  .nav-item.active {
    border-bottom-color: #2154a2;
  }

  .nav-item:hover {
    background: rgba(33, 84, 162, 0.05);
  }

  .nav-item:focus {
    outline: 2px solid #2154a2;
    outline-offset: -2px;
  }

  main {
    padding-top: 96px;
    padding-left: 1rem;
    padding-right: 1rem;
    min-height: 100vh;
  }

  .detail-container {
    max-width: 800px;
    margin: 0 auto;
  }

  .detail-header {
    margin-bottom: 2rem;
  }

  .back-btn {
    background: #f8f9fa;
    border: 1px solid #e3eaf6;
    color: #2154a2;
    padding: 0.75rem 1.5rem;
    border-radius: 8px;
    cursor: pointer;
    font-size: 0.9rem;
    font-weight: 500;
    transition: all 0.2s;
    margin-bottom: 1rem;
  }

  .back-btn:hover {
    background: #e9ecef;
    border-color: #2154a2;
  }

  .detail-header h1 {
    margin: 0;
    color: #2154a2;
    font-size: 2rem;
    font-weight: 600;
  }

  .user-card {
    background: #fff;
    border-radius: 12px;
    box-shadow: 0 4px 24px rgba(33,84,162,0.08);
    padding: 2rem;
  }

  .user-info {
    margin-bottom: 2rem;
  }

  .info-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 0;
    border-bottom: 1px solid #e3eaf6;
  }

  .info-row:last-child {
    border-bottom: none;
  }

  .info-row .label {
    font-weight: 600;
    color: #2c3e50;
    font-size: 1rem;
    min-width: 200px;
  }

  .value {
    color: #2c3e50;
    font-size: 1rem;
    font-weight: 500;
  }

  .uuid-text {
    font-family: 'SF Mono', Monaco, 'Cascadia Code', monospace;
    background: #f8f9fa;
    padding: 0.5rem 1rem;
    border-radius: 6px;
    color: #6c757d;
    font-size: 0.9rem;
  }

  .date-value {
    color: #4a5568;
    font-size: 1rem;
  }

  .score-badge {
    background: #e8f5e8;
    color: #2d7d2d;
    padding: 0.5rem 1rem;
    border-radius: 20px;
    font-weight: 600;
    font-size: 1rem;
  }

  .actions {
    display: flex;
    justify-content: center;
    padding-top: 1rem;
    border-top: 1px solid #e3eaf6;
  }

  .delete-btn {
    background: #dc3545;
    border: none;
    color: #fff;
    padding: 0.75rem 2rem;
    border-radius: 8px;
    cursor: pointer;
    font-size: 1rem;
    font-weight: 600;
    transition: all 0.2s;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .delete-btn:hover {
    background: #c82333;
    transform: translateY(-1px);
    box-shadow: 0 4px 12px rgba(220, 53, 69, 0.3);
  }

  .error-message {
    background: #fff;
    border-radius: 12px;
    box-shadow: 0 4px 24px rgba(33,84,162,0.08);
    padding: 3rem;
    text-align: center;
  }

  .error-message p {
    color: #6c757d;
    font-size: 1.2rem;
    margin-bottom: 1.5rem;
  }

  .rank-badge {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 40px;
    height: 40px;
    background: #2154a2;
    color: white;
    border-radius: 50%;
    font-weight: bold;
    font-size: 1.1rem;
  }

  @media (max-width: 768px) {
    .detail-container {
      max-width: 100%;
    }

    .user-card {
      padding: 1.5rem;
    }

    .info-row {
      flex-direction: column;
      align-items: flex-start;
      gap: 0.5rem;
    }

    .detail-header h1 {
      font-size: 1.5rem;
    }
  }
</style>
