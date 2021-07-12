<script lang="ts">
  import { domain } from '$lib/store'

  import { onMount } from 'svelte'

  import '../app.css'

  onMount(() => {
    const key = 'mail:domain'
    const saved = window.localStorage.getItem(key)
    if (saved) domain.set(saved)
    domain.subscribe((d) => window.localStorage.setItem(key, d))
  })
</script>

<main>
  <slot />
</main>

<style>
  main {
    width: 100%;
    padding: 2rem;
    max-width: 32rem;
    margin: 0 auto;
  }
</style>
