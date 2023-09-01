<script>
  import { page } from '$app/stores'
  import { browser } from '$app/environment'
  import { goto } from '$app/navigation'

  let queryParams = ''
  let value = ''

  function updateQueryParamsWithHistory() {
    if (!browser) return

    queryParams = 'newParams'

    const params = new URLSearchParams(window.location.search)

    params.set('q', queryParams)

    history.replaceState(
      history.state,
      '',
      decodeURIComponent(`${window.location.pathname}?${params}`),
    )
  }

  function updateQueryParamsWithGoto(value) {
    if (!browser) return

    queryParams = value

    const params = new URLSearchParams(window.location.search)

    params.set('q', queryParams)

    const destination = decodeURIComponent(`${window.location.pathname}?${params}`)

    goto(destination, {
      noScroll: true,
      replaceState: true,
      keepFocus: true,
    }).then(() => console.log('goto finished navigating to:', destination))
  }

  $: value && updateQueryParamsWithGoto(value)

  $: currentSearchParams = browser ? Object.fromEntries($page.url.searchParams) : null

  $: console.log('currentSearchParams', currentSearchParams)
</script>

<button on:click={updateQueryParamsWithHistory}>Update Query Params with `history`</button>

<p>Query Params: {queryParams}</p>

<input bind:value type="text" on:change={updateQueryParamsWithHistory} />

{#if browser}
  <p>currentSearchParams: {JSON.stringify(currentSearchParams)}</p>
{/if}
