<script lang="ts">
  import QuestionnaireFilter from '../components/QuestionnaireFilter.svelte';

  // Correction pour Svelte 5
  interface Props {
    setCurrentPage: (page: 'users' | 'questionnaires') => void;
  }

  let { setCurrentPage }: Props = $props();

  type Questionnaire = {
    uuid: string;
    creation: string;
    niveau: string;
    dateExam: string;
  };

  let questionnaires: Questionnaire[] = [
    { uuid: 'q1a2b3', creation: '2024-01-15', niveau: 'Débutant', dateExam: '2024-02-15' },
    { uuid: 'q4d5e6', creation: '2024-02-20', niveau: 'Intermédiaire', dateExam: '2024-03-20' },
    { uuid: 'q7g8h9', creation: '2024-03-10', niveau: 'Avancé', dateExam: '2024-04-10' },
    { uuid: 'q1k2l3', creation: '2024-01-25', niveau: 'Expert', dateExam: '2024-02-25' },
    { uuid: 'q4m5n6', creation: '2024-04-05', niveau: 'Débutant', dateExam: '2024-05-05' },
    { uuid: 'q7o8p9', creation: '2024-02-12', niveau: 'Intermédiaire', dateExam: '2024-03-12' },
    { uuid: 'q1q2r3', creation: '2024-03-18', niveau: 'Avancé', dateExam: '2024-04-18' },
    { uuid: 'q4s5t6', creation: '2024-01-08', niveau: 'Expert', dateExam: '2024-02-08' },
    { uuid: 'q7u8v9', creation: '2024-04-22', niveau: 'Débutant', dateExam: '2024-05-22' },
    { uuid: 'q1w2x3', creation: '2024-02-28', niveau: 'Intermédiaire', dateExam: '2024-03-28' },
    { uuid: 'q4y5z6', creation: '2024-03-05', niveau: 'Avancé', dateExam: '2024-04-05' },
    { uuid: 'q7a8b9', creation: '2024-01-30', niveau: 'Expert', dateExam: '2024-03-01' },
    { uuid: 'q1c2d3', creation: '2024-04-12', niveau: 'Débutant', dateExam: '2024-05-12' },
    { uuid: 'q4e5f6', creation: '2024-02-18', niveau: 'Intermédiaire', dateExam: '2024-03-18' },
    { uuid: 'q7g8h1', creation: '2024-03-25', niveau: 'Avancé', dateExam: '2024-04-25' },
    { uuid: 'q1i2j3', creation: '2024-01-12', niveau: 'Expert', dateExam: '2024-02-12' },
    { uuid: 'q4k5l6', creation: '2024-04-08', niveau: 'Débutant', dateExam: '2024-05-08' },
    { uuid: 'q7m8n9', creation: '2024-02-22', niveau: 'Intermédiaire', dateExam: '2024-03-22' },
    { uuid: 'q1o2p3', creation: '2024-03-15', niveau: 'Avancé', dateExam: '2024-04-15' },
    { uuid: 'q4q5r6', creation: '2024-01-28', niveau: 'Expert', dateExam: '2024-02-28' },
    { uuid: 'q7s8t9', creation: '2024-04-18', niveau: 'Débutant', dateExam: '2024-05-18' },
    { uuid: 'q1u2v3', creation: '2024-02-08', niveau: 'Intermédiaire', dateExam: '2024-03-08' },
    { uuid: 'q4w5x6', creation: '2024-03-22', niveau: 'Avancé', dateExam: '2024-04-22' },
    { uuid: 'q7y8z9', creation: '2024-01-18', niveau: 'Expert', dateExam: '2024-02-18' },
    { uuid: 'q1a3b4', creation: '2024-04-25', niveau: 'Débutant', dateExam: '2024-05-25' }
  ];

  let sortKey: keyof Questionnaire | null = $state(null);
  let sortDirection: 'asc' | 'desc' = $state('asc');

  let filterUuid = $state('');
  let filterCreationDateType = $state('any');
  let filterCreationDate = $state('');
  let filterNiveau = $state('any');
  let filterExamDateType = $state('any');
  let filterExamDate = $state('');
  let usersPerPage = $state(25);
  let currentPage = $state(1);

  let filteredQuestionnaires = $derived(questionnaires.filter(questionnaire => {
    if (filterUuid && !questionnaire.uuid.toLowerCase().includes(filterUuid.toLowerCase())) {
      return false;
    }

    if (filterCreationDateType !== 'any' && filterCreationDate) {
      const creationDate = new Date(questionnaire.creation);
      const targetDate = new Date(filterCreationDate);
      if (filterCreationDateType === 'before' && creationDate >= targetDate) return false;
      if (filterCreationDateType === 'after' && creationDate <= targetDate) return false;
    }

    if (filterNiveau !== 'any' && questionnaire.niveau !== filterNiveau) {
      return false;
    }

    if (filterExamDateType !== 'any' && filterExamDate) {
      const examDate = new Date(questionnaire.dateExam);
      const targetDate = new Date(filterExamDate);
      if (filterExamDateType === 'before' && examDate >= targetDate) return false;
      if (filterExamDateType === 'after' && examDate <= targetDate) return false;
    }

    return true;
  }));

  let sortedQuestionnaires = $derived(sortKey ? [...filteredQuestionnaires].toSorted((a, b) => {
    const valA = a[sortKey];
    const valB = b[sortKey];

    if (sortKey === 'creation' || sortKey === 'dateExam') {
      return sortDirection === 'asc'
        ? new Date(valA).getTime() - new Date(valB).getTime()
        : new Date(valB).getTime() - new Date(valA).getTime();
    }
    return String(valA).localeCompare(String(valB)) * (sortDirection === 'asc' ? 1 : -1);
  }) : filteredQuestionnaires);

  let totalPages = $derived(Math.ceil(sortedQuestionnaires.length / usersPerPage));

  let paginatedQuestionnaires = $derived.by(() => {
    const startIndex = (currentPage - 1) * usersPerPage;
    const endIndex = startIndex + usersPerPage;
    return sortedQuestionnaires.slice(startIndex, endIndex);
  });

  $effect(() => {
    if (currentPage > totalPages && totalPages > 0) {
      currentPage = 1;
    }
  });

  function sortTable(key: keyof Questionnaire) {
    if (sortKey === key) {
      sortDirection = sortDirection === 'asc' ? 'desc' : 'asc';
    } else {
      sortKey = key;
      sortDirection = 'asc';
    }
  }

  function getNiveauBadgeClass(niveau: string) {
    switch (niveau) {
      case 'Débutant': return 'niveau-debutant';
      case 'Intermédiaire': return 'niveau-intermediaire';
      case 'Avancé': return 'niveau-avance';

      default: return 'niveau-default';
    }
  }
</script>

<header>
  <nav>
    <button 
      type="button" 
      class="nav-item" 
      onclick={() => setCurrentPage('users')}
    >
      Users
    </button>
    <button 
      type="button" 
      class="nav-item active" 
      onclick={() => setCurrentPage('questionnaires')}
    >
      Questionnaires
    </button>
    <button 
      type="button" 
      class="nav-item"
    >
      Stats
    </button>
  </nav>
</header>

<main>
  <div class="table-container">
    <table>
      <thead>
        <tr>
          <th onclick={() => sortTable('uuid')}>
            <span class="header-content">
              <span class="header-text">UUID</span>
              {#if sortKey === 'uuid'}
                <span class="arrow">{sortDirection === 'asc' ? '↑' : '↓'}</span>
              {/if}
            </span>
          </th>
          <th class:active={sortKey === 'creation'} onclick={() => sortTable('creation')}>
            <span class="header-content">
              <span class="header-text">Date création</span>
              {#if sortKey === 'creation'}
                <span class="arrow">{sortDirection === 'asc' ? '↑' : '↓'}</span>
              {/if}
            </span>
          </th>
          <th class:active={sortKey === 'niveau'} onclick={() => sortTable('niveau')}>
            <span class="header-content">
              <span class="header-text">Niveau</span>
              {#if sortKey === 'niveau'}
                <span class="arrow">{sortDirection === 'asc' ? '↑' : '↓'}</span>
              {/if}
            </span>
          </th>
          <th class:active={sortKey === 'dateExam'} onclick={() => sortTable('dateExam')}>
            <span class="header-content">
              <span class="header-text">Date examen</span>
              {#if sortKey === 'dateExam'}
                <span class="arrow">{sortDirection === 'asc' ? '↑' : '↓'}</span>
              {/if}
            </span>
          </th>
        </tr>
      </thead>

      <tbody>
        {#each paginatedQuestionnaires as questionnaire (questionnaire.uuid)}
          <tr>
            <td>
              <span class="uuid-text">{questionnaire.uuid}</span>
            </td>
            <td class="date-col">{questionnaire.creation}</td>
            <td>
              <span class="niveau-badge {getNiveauBadgeClass(questionnaire.niveau)}">{questionnaire.niveau}</span>
            </td>
            <td class="date-col">{questionnaire.dateExam}</td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>

  <QuestionnaireFilter
    bind:filterUuid
    bind:filterCreationDateType
    bind:filterCreationDate
    bind:filterNiveau
    bind:filterExamDateType
    bind:filterExamDate
    bind:usersPerPage
    bind:currentPage
    resultCount={sortedQuestionnaires.length}
    totalPages={totalPages}
  />
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

  :global(*) {
    scrollbar-width: auto;
    scrollbar-color: auto;
  }

  :global(*::-webkit-scrollbar) {
    width: auto;
    height: auto;
  }

  :global(*::-webkit-scrollbar-track) {
    background: auto;
  }

  :global(*::-webkit-scrollbar-thumb) {
    background: auto;
    border-radius: auto;
  }

  :global(*::-webkit-scrollbar-thumb:hover) {
    background: auto;
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
    display: flex;
    height: 100vh;
    padding-top: 96px;
    padding-left: 1rem;
    padding-right: 1rem;
    gap: 1rem;
    overflow-y: auto;
  }

  .table-container {
    flex: 1;
    background: #fff;
    padding: 2rem 1.5rem 1.5rem;
    box-shadow: 0 4px 24px rgba(33,84,162,0.08);
    border-radius: 12px 0 0 12px;
    min-height: fit-content;
    overflow: auto;
    max-height: calc(100vh - 128px);
  }

  table {
    width: 100%;
    border-collapse: collapse;
  }

  th {
    background: #2154a2;
    color: #fff;
    padding: 0.75rem 1rem;
    text-align: left;
    cursor: pointer;
    font-weight: 700;
    font-size: 0.9rem;
    transition: background 0.2s;
    position: sticky;
    top: 0;
    z-index: 10;
  }

  th:hover {
    background: #133a6a;
  }

  th.active {
    background: #133a6a;
  }

  td {
    padding: 0.75rem 1rem;
    border-bottom: 1px solid #e3eaf6;
    color: #2c3e50;
    font-size: 0.9rem;
    background: #fff;
    position: relative;
    z-index: 1;
  }

  tr:hover td {
    background: #f8f9fa;
  }

  tr:last-child td {
    border-bottom: none;
  }

  .header-content {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
  }

  .arrow {
    margin-left: 8px;
    color: #fff;
    font-weight: bold;
  }

  .uuid-text {
    font-family: 'SF Mono', Monaco, 'Cascadia Code', monospace;
    background: #f8f9fa;
    padding: 0.25rem 0.5rem;
    border-radius: 4px;
    color: #6c757d;
    font-size: 0.8rem;
  }

  .date-col {
    font-family: 'SF Mono', Monaco, 'Cascadia Code', monospace;
    color: #4a5568;
    font-size: 0.85rem;
  }

  .niveau-badge {
    padding: 0.25rem 0.75rem;
    border-radius: 20px;
    font-weight: 600;
    font-size: 0.85rem;
  }

  .niveau-debutant {
    background: #e8f5e8;
    color: #2d7d2d;
  }

  .niveau-intermediaire {
    background: #fff3cd;
    color: #856404;
  }

  .niveau-avance {
    background: #d1ecf1;
    color: #0c5460;
  }

  .niveau-expert {
    background: #f8d7da;
    color: #721c24;
  }

  .niveau-default {
    background: #e9ecef;
    color: #495057;
  }

  @media (max-width: 768px) {
    main {
      flex-direction: column;
      padding-top: 72px;
    }
    
    .table-container {
      border-radius: 12px 12px 0 0;
      max-height: calc(100vh - 100px);
    }
  }
</style>
