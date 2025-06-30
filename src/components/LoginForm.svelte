<script lang="ts">
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  let username = '';
  let password = '';
  let error = '';

  function handleSubmit(event: Event) {
    event.preventDefault();
    error = '';
    if (!username || !password) {
      error = 'Please enter both username and password.';
      return;
    }
    // Simulate login success (replace with real auth logic)
    if (username === 'admin' && password === 'admin') {
      dispatch('login');
    } else {
      error = 'In case of a login failure, contact your system admin.';
    }
  }
</script>

<form class="login-card" on:submit|preventDefault={handleSubmit}>
  <h2>Sign in</h2>
  <div class="field">
    <label for="username">Username</label>
    <input id="username" type="text" bind:value={username} required autocomplete="username" />
  </div>
  <div class="field">
    <label for="password">Password</label>
    <input id="password" type="password" bind:value={password} required autocomplete="current-password" />
  </div>
  {#if error}
    <div class="error">{error}</div>
  {/if}
  <button type="submit">Log in</button>
</form>

  
<style>
  .login-card {
    background: #fff;
    border-radius: 16px;
    box-shadow: 0 4px 24px rgba(33, 84, 162, 0.10);
    padding: 2.5rem 2.5rem 2rem 2.5rem;
    width: 360px;
    max-width: 90vw;
    display: flex;
    flex-direction: column;
    gap: 1.2rem;
    align-items: stretch;
  }
  h2 {
    color: #2154a2;
    margin-bottom: 1rem;
    text-align: left; /* Change from center to left */
  }
  .field {
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
    text-align: left; /* Ensure label and input are left-aligned */
  }
  label {
    font-weight: 500;
    color: #2154a2;
    text-align: left;
  }
  input {
    border: 1.5px solid #2154a2;
    border-radius: 6px;
    padding: 0.6rem 0.9rem;
    font-size: 1rem;
    background: #fff;
    color: #222;
    outline: none;
    transition: border-color 0.2s;
    text-align: left;
  }
  input:focus {
    border-color: #133a6a;
    background: #f5f8fa;
  }
  .error {
    color: #d32f2f;
    background: #fbe9e7;
    border-radius: 4px;
    padding: 0.5rem;
    font-size: 0.95rem;
    text-align: left; /* Error message left-aligned */
  }
  button {
    background: #2154a2;
    color: #fff;
    border: none;
    border-radius: 6px;
    padding: 0.8rem;
    font-size: 1.1rem;
    font-weight: 600;
    cursor: pointer;
    width: 100%;
    transition: background 0.2s;
    margin-top: 0.5rem;
    text-align: center;
  }
  button:hover {
    background: #133a6a;
  }
  @media (max-width: 500px) {
    .login-card {
      width: 95vw;
      padding: 1.2rem 0.5rem;
    }
  }
</style>


