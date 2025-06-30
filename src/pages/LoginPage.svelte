<script lang="ts">
  import LoginForm from '../components/LoginForm.svelte';
  export let onLogin: () => void;
</script>

<div class="container">
  <LoginForm on:login={onLogin} />
</div>

<style>
  :global(html, body) {
    height: 100%;
    margin: 0;
    padding: 0;
    background: #f5f8fa;
  }

  .container {
    display: flex;
    align-items: center;
    justify-content: center;
  }
</style>


