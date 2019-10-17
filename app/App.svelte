<script>
  import { onMount } from 'svelte'

  let users = []

  onMount(async () => {
    const res = await fetch(`https://randomuser.me/api/?page=1&results=25`)
    const response = await res.json()
    users = response.results
  })
</script>

<style>
  .users {
    width: 100%;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-gap: 8px;
  }

  figure,
  img {
    width: 100%;
    margin: 0;
  }
</style>

<div class="users">
  {#each users as user}
    <figure>
      <img src={user.picture.large} alt={user.name.first} />
      <figcaption>{user.name.first}</figcaption>
    </figure>
  {:else}
    <!-- this block renders when users.length === 0 -->
    <p>loading...</p>
  {/each}
</div>
