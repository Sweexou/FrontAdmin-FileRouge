<script lang="ts">
  import FilterPanel from '../components/FilterPanel.svelte';

  interface Props {
    setCurrentPage: (page: 'users' | 'questionnaires' | 'userDetail') => void;
    setSelectedUser: (user: User) => void;
  }
  let { setCurrentPage, setSelectedUser }: Props = $props();

  type User = {
    uuid: string;
    classement: number;
    name: string;
    creation: string;
    score: number;
  };

  let users: User[] = [
    { uuid: 'wfqzck', classement: 1, name: 'Grace Martin', creation: '2020-03-02', score: 134 },
    { uuid: 'tlfd5k', classement: 2, name: 'Grace Dupont', creation: '2020-07-11', score: 127 },
    { uuid: 'w654xe', classement: 3, name: 'Grace Wilson', creation: '2023-03-16', score: 114 },
    { uuid: 'nlw3t6', classement: 4, name: 'David Martin', creation: '2020-10-16', score: 124 },
    { uuid: 'n3p03k', classement: 5, name: 'Jack Johnson', creation: '2024-02-25', score: 67 },
    { uuid: 'a7b2c9', classement: 6, name: 'Alice Brown', creation: '2021-05-14', score: 98 },
    { uuid: 'x3y8z1', classement: 7, name: 'Bob Davis', creation: '2022-11-03', score: 156 },
    { uuid: 'm4n7p2', classement: 8, name: 'Eva Miller', creation: '2021-08-19', score: 89 },
    { uuid: 'q5r9s3', classement: 9, name: 'Frank Moore', creation: '2023-01-07', score: 142 },
    { uuid: 't6u1v4', classement: 10, name: 'Hugo Smith', creation: '2020-12-22', score: 76 },
    { uuid: 'w7x2y5', classement: 11, name: 'Ivy Wilson', creation: '2022-04-15', score: 103 },
    { uuid: 'z8a3b6', classement: 12, name: 'Jack Brown', creation: '2021-09-28', score: 118 },
    { uuid: 'c9d4e7', classement: 13, name: 'Alice Johnson', creation: '2023-06-11', score: 85 },
    { uuid: 'f1g5h8', classement: 14, name: 'Bob Rossi', creation: '2020-02-17', score: 139 },
    { uuid: 'i2j6k9', classement: 15, name: 'Carla Davis', creation: '2024-01-04', score: 92 },
    { uuid: 'l3m7n1', classement: 16, name: 'David Wilson', creation: '2021-07-20', score: 107 },
    { uuid: 'o4p8q2', classement: 17, name: 'Eva Smith', creation: '2022-12-08', score: 73 },
    { uuid: 'r5s9t3', classement: 18, name: 'Frank Miller', creation: '2023-03-25', score: 125 },
    { uuid: 'u6v1w4', classement: 19, name: 'Grace Johnson', creation: '2020-08-12', score: 94 },
    { uuid: 'x7y2z5', classement: 20, name: 'Hugo Brown', creation: '2021-11-29', score: 111 },
    { uuid: 'a8b3c6', classement: 21, name: 'Ivy Davis', creation: '2022-05-16', score: 88 },
    { uuid: 'd9e4f7', classement: 22, name: 'Jack Martin', creation: '2023-10-02', score: 133 },
    { uuid: 'g1h5i8', classement: 23, name: 'Alice Moore', creation: '2020-04-19', score: 79 },
    { uuid: 'j2k6l9', classement: 24, name: 'Bob Wilson', creation: '2024-03-06', score: 146 },
    { uuid: 'm3n7o1', classement: 25, name: 'Carla Smith', creation: '2021-06-23', score: 101 },
    { uuid: 'p4q8r2', classement: 26, name: 'David Brown', creation: '2022-09-10', score: 84 },
    { uuid: 's5t9u3', classement: 27, name: 'Eva Johnson', creation: '2023-12-27', score: 119 },
    { uuid: 'v6w1x4', classement: 28, name: 'Frank Davis', creation: '2020-01-14', score: 96 },
    { uuid: 'y7z2a5', classement: 29, name: 'Grace Miller', creation: '2021-04-01', score: 112 },
    { uuid: 'b8c3d6', classement: 30, name: 'Hugo Wilson', creation: '2022-07-18', score: 87 },
    { uuid: 'e9f4g7', classement: 31, name: 'Ivy Moore', creation: '2023-02-04', score: 128 },
    { uuid: 'h1i5j8', classement: 32, name: 'Jack Smith', creation: '2020-05-21', score: 75 },
    { uuid: 'k2l6m9', classement: 33, name: 'Alice Davis', creation: '2024-04-08', score: 140 },
    { uuid: 'n3o7p1', classement: 34, name: 'Bob Miller', creation: '2021-08-25', score: 93 },
    { uuid: 'q4r8s2', classement: 35, name: 'Carla Brown', creation: '2022-11-12', score: 106 },
    { uuid: 't5u9v3', classement: 36, name: 'David Johnson', creation: '2023-04-29', score: 82 },
    { uuid: 'w6x1y4', classement: 37, name: 'Eva Wilson', creation: '2020-09-16', score: 115 },
    { uuid: 'z7a2b5', classement: 38, name: 'Frank Moore', creation: '2021-12-03', score: 99 },
    { uuid: 'c8d3e6', classement: 39, name: 'Grace Smith', creation: '2022-03-20', score: 123 },
    { uuid: 'f9g4h7', classement: 40, name: 'Hugo Davis', creation: '2023-08-07', score: 78 },
    { uuid: 'i1j5k8', classement: 41, name: 'Ivy Miller', creation: '2020-11-24', score: 135 },
    { uuid: 'l2m6n9', classement: 42, name: 'Jack Brown', creation: '2024-02-10', score: 91 },
    { uuid: 'o3p7q1', classement: 43, name: 'Alice Wilson', creation: '2021-05-28', score: 108 },
    { uuid: 'r4s8t2', classement: 44, name: 'Bob Johnson', creation: '2022-08-14', score: 86 },
    { uuid: 'u5v9w3', classement: 45, name: 'Carla Moore', creation: '2023-01-01', score: 121 },
    { uuid: 'x6y1z4', classement: 46, name: 'David Smith', creation: '2020-06-18', score: 97 },
    { uuid: 'a7b2c5', classement: 47, name: 'Eva Davis', creation: '2021-09-05', score: 113 },
    { uuid: 'd8e3f6', classement: 48, name: 'Frank Miller', creation: '2022-12-22', score: 80 },
    { uuid: 'g9h4i7', classement: 49, name: 'Grace Brown', creation: '2023-05-09', score: 137 },
    { uuid: 'j1k5l8', classement: 50, name: 'Hugo Wilson', creation: '2020-10-26', score: 95 },
    { uuid: 'm2n6o9', classement: 51, name: 'Ivy Johnson', creation: '2024-01-13', score: 109 },
    { uuid: 'p3q7r1', classement: 52, name: 'Jack Moore', creation: '2021-04-30', score: 83 },
    { uuid: 's4t8u2', classement: 53, name: 'Alice Smith', creation: '2022-07-17', score: 126 },
    { uuid: 'v5w9x3', classement: 54, name: 'Bob Davis', creation: '2023-10-04', score: 77 },
    { uuid: 'y6z1a4', classement: 55, name: 'Carla Miller', creation: '2020-03-21', score: 144 },
    { uuid: 'b7c2d5', classement: 56, name: 'David Brown', creation: '2021-06-08', score: 90 },
    { uuid: 'e8f3g6', classement: 57, name: 'Eva Wilson', creation: '2022-09-25', score: 105 },
    { uuid: 'h9i4j7', classement: 58, name: 'Frank Johnson', creation: '2023-12-12', score: 81 },
    { uuid: 'k1l5m8', classement: 59, name: 'Grace Moore', creation: '2020-07-29', score: 117 },
    { uuid: 'n2o6p9', classement: 60, name: 'Hugo Smith', creation: '2024-03-16', score: 98 },
    { uuid: 'q3r7s1', classement: 61, name: 'Ivy Davis', creation: '2021-08-03', score: 122 },
    { uuid: 't4u8v2', classement: 62, name: 'Jack Miller', creation: '2022-11-20', score: 74 },
    { uuid: 'w5x9y3', classement: 63, name: 'Alice Brown', creation: '2023-02-07', score: 131 },
    { uuid: 'z6a1b4', classement: 64, name: 'Bob Wilson', creation: '2020-05-26', score: 89 },
    { uuid: 'c7d2e5', classement: 65, name: 'Carla Johnson', creation: '2021-08-13', score: 104 },
    { uuid: 'f8g3h6', classement: 66, name: 'David Moore', creation: '2022-01-30', score: 86 },
    { uuid: 'i9j4k7', classement: 67, name: 'Eva Smith', creation: '2023-06-17', score: 116 },
    { uuid: 'l1m5n8', classement: 68, name: 'Frank Davis', creation: '2020-09-04', score: 92 },
    { uuid: 'o2p6q9', classement: 69, name: 'Grace Miller', creation: '2024-04-21', score: 129 },
    { uuid: 'r3s7t1', classement: 70, name: 'Hugo Brown', creation: '2021-07-08', score: 85 },
    { uuid: 'u4v8w2', classement: 71, name: 'Ivy Wilson', creation: '2022-10-25', score: 110 },
    { uuid: 'x5y9z3', classement: 72, name: 'Jack Johnson', creation: '2023-03-14', score: 79 },
    { uuid: 'a6b1c4', classement: 73, name: 'Alice Moore', creation: '2020-08-01', score: 138 },
    { uuid: 'd7e2f5', classement: 74, name: 'Bob Smith', creation: '2021-10-18', score: 93 },
    { uuid: 'g8h3i6', classement: 75, name: 'Carla Davis', creation: '2022-05-05', score: 107 },
    { uuid: 'j9k4l7', classement: 76, name: 'David Miller', creation: '2023-09-22', score: 82 },
    { uuid: 'm1n5o8', classement: 77, name: 'Eva Brown', creation: '2020-12-09', score: 124 },
    { uuid: 'p2q6r9', classement: 78, name: 'Frank Wilson', creation: '2024-05-26', score: 96 },
    { uuid: 's3t7u1', classement: 79, name: 'Grace Johnson', creation: '2021-02-13', score: 114 },
    { uuid: 'v4w8x2', classement: 80, name: 'Hugo Moore', creation: '2022-06-30', score: 88 },
    { uuid: 'y5z9a3', classement: 81, name: 'Ivy Smith', creation: '2023-11-17', score: 132 },
    { uuid: 'b6c1d4', classement: 82, name: 'Jack Davis', creation: '2020-04-05', score: 91 },
    { uuid: 'e7f2g5', classement: 83, name: 'Alice Miller', creation: '2021-09-22', score: 106 },
    { uuid: 'h8i3j6', classement: 84, name: 'Bob Brown', creation: '2022-02-08', score: 84 },
    { uuid: 'k9l4m7', classement: 85, name: 'Carla Wilson', creation: '2023-07-27', score: 119 },
    { uuid: 'n1o5p8', classement: 86, name: 'David Johnson', creation: '2020-11-14', score: 97 },
    { uuid: 'q2r6s9', classement: 87, name: 'Eva Moore', creation: '2024-06-01', score: 112 },
    { uuid: 't3u7v1', classement: 88, name: 'Frank Smith', creation: '2021-03-20', score: 87 },
    { uuid: 'w4x8y2', classement: 89, name: 'Grace Davis', creation: '2022-08-07', score: 125 },
    { uuid: 'z5a9b3', classement: 90, name: 'Hugo Miller', creation: '2023-12-24', score: 78 },
    { uuid: 'c6d1e4', classement: 91, name: 'Ivy Brown', creation: '2020-07-11', score: 135 },
    { uuid: 'f7g2h5', classement: 92, name: 'Jack Wilson', creation: '2021-11-28', score: 90 },
    { uuid: 'i8j3k6', classement: 93, name: 'Alice Johnson', creation: '2022-04-16', score: 108 },
    { uuid: 'l9m4n7', classement: 94, name: 'Bob Moore', creation: '2023-08-03', score: 83 },
    { uuid: 'o1p5q8', classement: 95, name: 'Carla Smith', creation: '2020-01-20', score: 127 },
    { uuid: 'r2s6t9', classement: 96, name: 'David Davis', creation: '2024-04-07', score: 95 },
    { uuid: 'u3v7w1', classement: 97, name: 'Eva Miller', creation: '2021-06-24', score: 111 },
    { uuid: 'x4y8z2', classement: 98, name: 'Frank Brown', creation: '2022-09-11', score: 86 },
    { uuid: 'a5b9c3', classement: 99, name: 'Grace Wilson', creation: '2023-01-28', score: 120 },
    { uuid: 'd6e1f4', classement: 100, name: 'Hugo Johnson', creation: '2020-06-15', score: 94 },
    { uuid: 'g7h2i5', classement: 101, name: 'Ivy Moore', creation: '2021-10-02', score: 118 },
    { uuid: 'j8k3l6', classement: 102, name: 'Jack Smith', creation: '2022-03-21', score: 81 },
    { uuid: 'm9n4o7', classement: 103, name: 'Alice Davis', creation: '2023-06-08', score: 133 },
    { uuid: 'p1q5r8', classement: 104, name: 'Bob Miller', creation: '2020-09-25', score: 89 },
    { uuid: 's2t6u9', classement: 105, name: 'Carla Brown', creation: '2024-02-12', score: 105 },
    { uuid: 'v3w7x1', classement: 106, name: 'David Wilson', creation: '2021-05-01', score: 87 },
    { uuid: 'y4z8a2', classement: 107, name: 'Eva Johnson', creation: '2022-07-18', score: 115 },
    { uuid: 'b5c9d3', classement: 108, name: 'Frank Moore', creation: '2023-10-05', score: 92 },
    { uuid: 'e6f1g4', classement: 109, name: 'Grace Smith', creation: '2020-02-22', score: 128 },
    { uuid: 'h7i2j5', classement: 110, name: 'Hugo Davis', creation: '2021-07-11', score: 85 },
    { uuid: 'k8l3m6', classement: 111, name: 'Ivy Miller', creation: '2022-11-28', score: 109 },
    { uuid: 'n9o4p7', classement: 112, name: 'Jack Brown', creation: '2023-04-16', score: 80 },
    { uuid: 'q1r5s8', classement: 113, name: 'Alice Wilson', creation: '2020-08-03', score: 136 },
    { uuid: 't2u6v9', classement: 114, name: 'Bob Johnson', creation: '2024-03-21', score: 93 },
    { uuid: 'w3x7y1', classement: 115, name: 'Carla Moore', creation: '2021-06-08', score: 107 },
    { uuid: 'z4a8b2', classement: 116, name: 'David Smith', creation: '2022-08-25', score: 84 },
    { uuid: 'c5d9e3', classement: 117, name: 'Eva Davis', creation: '2023-11-12', score: 121 },
    { uuid: 'f6g1h4', classement: 118, name: 'Frank Miller', creation: '2020-04-29', score: 96 },
    { uuid: 'i7j2k5', classement: 119, name: 'Grace Brown', creation: '2021-08-16', score: 113 },
    { uuid: 'l8m3n6', classement: 120, name: 'Hugo Wilson', creation: '2022-12-03', score: 88 }
  ];


  let sortKey: keyof User | null = $state(null);
  let sortDirection: 'asc' | 'desc' = $state('asc');

  let filterName = $state('');
  let filterDateType = $state('any');
  let filterDate = $state('');
  let filterScoreType = $state('any');
  let filterScoreMin = $state('');
  let filterScoreMax = $state('');
  let filterRankType = $state('any');
  let filterRankMin = $state('');
  let filterRankMax = $state('');
  let usersPerPage = $state(25);
  let currentPage = $state(1);

  let filteredUsers = $derived(users.filter(user => {
    if (filterName && !user.name.toLowerCase().includes(filterName.toLowerCase())) {
      return false;
    }

    if (filterDateType !== 'any' && filterDate) {
      const userDate = new Date(user.creation);
      const targetDate = new Date(filterDate);
      if (filterDateType === 'before' && userDate >= targetDate) return false;
      if (filterDateType === 'after' && userDate <= targetDate) return false;
    }

    if (filterScoreType !== 'any') {
      if (filterScoreType === 'between' && (filterScoreMin || filterScoreMax)) {
        const min = filterScoreMin ? parseInt(filterScoreMin) : -Infinity;
        const max = filterScoreMax ? parseInt(filterScoreMax) : Infinity;
        if (user.score < min || user.score > max) return false;
      }
      if (filterScoreType === 'greater' && filterScoreMin) {
        if (user.score <= parseInt(filterScoreMin)) return false;
      }
      if (filterScoreType === 'less' && filterScoreMin) {
        if (user.score >= parseInt(filterScoreMin)) return false;
      }
    }

    if (filterRankType !== 'any') {
      if (filterRankType === 'between' && (filterRankMin || filterRankMax)) {
        const min = filterRankMin ? parseInt(filterRankMin) : -Infinity;
        const max = filterRankMax ? parseInt(filterRankMax) : Infinity;
        if (user.classement < min || user.classement > max) return false;
      }
      if (filterRankType === 'greater' && filterRankMin) {
        if (user.classement <= parseInt(filterRankMin)) return false;
      }
      if (filterRankType === 'less' && filterRankMin) {
        if (user.classement >= parseInt(filterRankMin)) return false;
      }
    }

    return true;
  }));

  let sortedUsers = $derived(sortKey ? [...filteredUsers].toSorted((a, b) => {
    const valA = a[sortKey];
    const valB = b[sortKey];

    if (typeof valA === 'number' && typeof valB === 'number') {
      return sortDirection === 'asc' ? valA - valB : valB - valA;
    }
    if (sortKey === 'creation') {
      return sortDirection === 'asc'
        ? new Date(valA).getTime() - new Date(valB).getTime()
        : new Date(valB).getTime() - new Date(valA).getTime();
    }
    return String(valA).localeCompare(String(valB)) * (sortDirection === 'asc' ? 1 : -1);
  }) : filteredUsers);

  let totalPages = $derived(Math.ceil(sortedUsers.length / usersPerPage));

  let paginatedUsers = $derived.by(() => {
    const startIndex = (currentPage - 1) * usersPerPage;
    const endIndex = startIndex + usersPerPage;
    return sortedUsers.slice(startIndex, endIndex);
  });


  // Reset page when filters change or users per page changes
  $effect(() => {
    if (currentPage > totalPages && totalPages > 0) {
      currentPage = 1;
    }
  });

  function selectUser(user: User) {
    // Ajout des données manquantes
    const completeUser = {
      ...user,
      username: user.name,
      email: `${user.name.toLowerCase().replace(' ', '.')}@example.com`,
      lastConnection: '2024-06-29'
    };
    setSelectedUser(completeUser);
    setCurrentPage('userDetail');
  }

  function sortTable(key: keyof User) {
    if (key === 'uuid') return;
    
    if (sortKey === key) {
      sortDirection = sortDirection === 'asc' ? 'desc' : 'asc';
    } else {
      sortKey = key;
      sortDirection = 'asc';
    }
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
          <th class="uuid-col">UUID</th>
          <th class:active={sortKey === 'classement'} onclick={() => sortTable('classement')}>
            <span class="header-content">
              <span class="header-text">Classement</span>
              {#if sortKey === 'classement'}
                <span class="arrow">{sortDirection === 'asc' ? '↑' : '↓'}</span>
              {/if}
            </span>
          </th>
          <th class:active={sortKey === 'name'} onclick={() => sortTable('name')}>
            <span class="header-content">
              <span class="header-text">Nom</span>
              {#if sortKey === 'name'}
                <span class="arrow">{sortDirection === 'asc' ? '↑' : '↓'}</span>
              {/if}
            </span>
          </th>
          <th class:active={sortKey === 'creation'} onclick={() => sortTable('creation')} class="date-col">
            <span class="header-content">
              <span class="header-text">Date création</span>
              {#if sortKey === 'creation'}
                <span class="arrow">{sortDirection === 'asc' ? '↑' : '↓'}</span>
              {/if}
            </span>
          </th>
          <th class:active={sortKey === 'score'} onclick={() => sortTable('score')}>
            <span class="header-content">
              <span class="header-text">Score</span>
              {#if sortKey === 'score'}
                <span class="arrow">{sortDirection === 'asc' ? '↑' : '↓'}</span>
              {/if}
            </span>
          </th>
        </tr>
      </thead>

      <tbody>
        {#each paginatedUsers as user (user.uuid)}
          <tr onclick={() => selectUser(user)} class="clickable-row">
            <td class="uuid-col">
              <span class="uuid-text">{user.uuid}</span>
            </td>
            <td>
              <span class="rank-badge">{user.classement}</span>
            </td>
            <td class="name-col">{user.name}</td>
            <td class="date-col">{user.creation}</td>
            <td>
              <span class="score-badge">{user.score}</span>
            </td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>

  <FilterPanel
    bind:filterName
    bind:filterDateType
    bind:filterDate
    bind:filterScoreType
    bind:filterScoreMin
    bind:filterScoreMax
    bind:filterRankType
    bind:filterRankMin
    bind:filterRankMax
    bind:usersPerPage
    bind:currentPage
    resultCount={sortedUsers.length}
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

  /* Reset des scrollbars personnalisées */
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

  .clickable-row {
    cursor: pointer;
    transition: all 0.2s;
  }

  .clickable-row:hover {
    background: #f0f6fd !important;
    transform: translateY(-1px);
    box-shadow: 0 2px 8px rgba(33,84,162,0.1);
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

  .rank-badge {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 30px;
    height: 30px;
    background: #2154a2;
    color: white;
    border-radius: 50%;
    font-weight: bold;
    font-size: 0.85rem;
  }

  .score-badge {
    background: #e8f5e8;
    color: #2d7d2d;
    padding: 0.25rem 0.75rem;
    border-radius: 20px;
    font-weight: 600;
    font-size: 0.85rem;
  }

  .uuid-text {
    font-family: 'SF Mono', Monaco, 'Cascadia Code', monospace;
    background: #f8f9fa;
    padding: 0.25rem 0.5rem;
    border-radius: 4px;
    color: #6c757d;
    font-size: 0.8rem;
  }

  .name-col {
    font-weight: 500;
    color: #1a202c;
  }

  @media (max-width: 768px) {
    main {
      flex-direction: column;
      padding-top: 72px;
    }
    
    .table-container {
      border-radius: 12px 12px 0 0;
    }
  }
</style>
