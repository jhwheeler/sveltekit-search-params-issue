<script>
  import { page } from '$app/stores'
	import { browser } from '$app/environment'

  let queryParams = ''

  const updateQueryParams = () => {
    queryParams = 'newParams'
    const params = new URLSearchParams(window.location.search)
    params.set('q', queryParams)
    history.replaceState(
      history.state,
      '',
      decodeURIComponent(`${window.location.pathname}?${params}`),
    )
  }

	$: currentSearchParams = browser ? Object.fromEntries($page.url.searchParams) : null

	$: console.log('currentSearchParams', currentSearchParams)
</script>

<button on:click={updateQueryParams}>Update Query Params</button>
<p>Query Params: {queryParams}</p>

{#if browser}
  <p>currentSearchParams: {JSON.stringify(currentSearchParams)}</p>
{/if}