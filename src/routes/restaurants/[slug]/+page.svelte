<script>
  import { get } from "$lib/dao/categories";

	/** @type {import('./$types').PageData} */
	export let data;

  const category = get(data.category);
</script>

<svelte:head>
  <title>Our favourite places - {data.name}</title>
</svelte:head>

<h1 class="mb-4 text-2xl font-bold leading-none">{data.name}</h1>

<div>
  <table class="text-sm text-left">
    <tr class="border-b">
      <th scope="row" class="px-6 py-3 font-medium bg-gray-50">Category</th>
      <td class="px-6 py-3">{category.displayName}</td>
    </tr>
    {#if data.website}
      <tr class="border-b">
        <th scope="row" class="px-6 py-3 font-medium bg-gray-50">Website</th>
        <td class="px-6 py-3"><a href="{data.website}">{data.website}</a></td>
      </tr>
    {/if}
    {#if data.source}
      <tr >
        <th scope="row" class="px-6 py-3 font-medium bg-gray-50">How we found it</th>
        <td class="px-6 py-3">{data.source}</td>
      </tr>
    {/if}
  </table>

  {#if data.menuItemsTried}
    <div class="my-4">
      <h2 class="mb-2 text-lg font-bold leading-none">Menu items we've tried</h2>
      <ul class="ml-2 list-disc list-inside">
        {#each data.menuItemsTried as menuItem}
          <li>{menuItem}</li>
        {/each}
      </ul>
    </div>
  {/if}
  
  {#if data.pageContent}
    <article class="mt-6 prose">
      {#each data.pageContent as contentElement}
        {#if contentElement.type === "paragraph"}
          <p>{contentElement.value}</p>
        {/if}
      {/each}
    </article>
  {/if}
</div>
