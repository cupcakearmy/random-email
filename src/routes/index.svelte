<script lang="ts">
  import copy from 'copy-to-clipboard'
  import { Button, TextField, Headline, Chip } from 'attractions'
  import { domain } from '$lib/store'

  let chosen: string | null = null

  function randomChar(alphabet = 'abcdefghijklmnopqrstuvwxyz'): string {
    return alphabet[Math.floor(Math.random() * alphabet.length)]
  }
  function rand(length = 8): string {
    if (length === 0) return ''
    return randomChar() + rand(length - 1)
  }

  function generate() {
    chosen = rand(16) + '@' + $domain
    copy(chosen)
  }
</script>

<Headline>Random Email</Headline>
<p>Generate random email addresses for a given domain</p>

<br />
<TextField outline label="Domain" type="text" bind:value={$domain} withItem>
  <div class="item">@</div>
</TextField>
<br />

<Button filled on:click={generate}>Generate & Copy</Button>

{#if chosen}
  <br />
  <TextField outline label="Generated" type="email" readonly value={chosen} />
  <br />
  <Chip small>Copied to clipboard ✔️</Chip>
{/if}
