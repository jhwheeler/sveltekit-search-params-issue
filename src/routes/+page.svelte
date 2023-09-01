<script>
  import { page } from '$app/stores'
  import { browser } from '$app/environment'
  import { goto } from '$app/navigation'

  let value = ''

  function updateQueryParamsWithGoto(value) {
    if (!browser) return

    const params = new URLSearchParams(window.location.search)

    params.set('q', value)

    const destination = decodeURIComponent(`${window.location.pathname}?${params}`)

    goto(destination, {
      noScroll: true,
      replaceState: true,
      keepFocus: true,
    }).then(() => console.log('goto finished navigating to:', destination))
  }

  $: value && updateQueryParamsWithGoto(value)

  $: queryParams = $page.url.searchParams.get('q') || ''
</script>

<label for="input">Update query params:</label>
<input id="input" bind:value type="text" />

<p>Query Params: {queryParams}</p>
