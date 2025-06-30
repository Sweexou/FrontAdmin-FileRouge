<script lang="ts">
  import LoginForm from '../components/LoginForm.svelte';
  
  // Correction pour Svelte 5
  interface Props {
    onLogin: () => void;
  }

  let { onLogin }: Props = $props();
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
