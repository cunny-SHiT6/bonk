<script lang="ts">
  import danbooru from "danbooru";
  const booru = new danbooru();

  let page = 1;
  let take = 20;
  let cunny = "";
  let posts = [];

  async function getCunny() {
    posts = (await booru
      .posts({ tags: cunny, page, limit: take })
      .then((res) =>
        res.map((p) => ({ tags: p.tag_string, url: p.file_url }))
      )) as Array<{ tags?: string; url?: string }>;
  }
</script>

<main class="flex flex-col items-center justify-center">
  <form
    class="flex items-center gap-2 py-8"
    on:submit|preventDefault={getCunny}
  >
    <label for="">page</label>
    <input type="number" bind:value={page} placeholder="page" />
    <label for="">take</label>
    <input type="number" bind:value={take} placeholder="take" />
    <label for="">cunny</label>
    <input type="text" bind:value={cunny} placeholder="cunny" />
    <button action="submit"> Get Cunny </button>
  </form>

  {#each posts as post, index}
    <div
      class="flex flex-col items-center rounded-xl bg-slate-100 p-2 text-center shadow-xl"
    >
      <div>
        <p class="text-2xl">{index + 1}</p>
        <p>{post.tags}</p>
      </div>

      <img src={post.url} width="420" alt="cunny" />
    </div>
  {/each}

  {#if !posts.length}
    <p>No cunny yet</p>
  {/if}
</main>

<style lang="postcss">
  input,
  button {
    @apply rounded border border-gray-500 p-2;
  }
</style>
