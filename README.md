# SvelteKit Query Params Issue

This repository contains a minimal reproducible example of an issue with SvelteKit's `$page` store not updating correctly when you manually set the query parameters in the URL using `history`.

## Description

In our SvelteKit application, we have a function that updates the query parameters in the URL using the `history` API. However, after updating the query parameters, the `$page` store does not reflect these changes. This behavior is inconsistent with the expected behavior, where the `$page` store should update to reflect the current state of the page, including the query parameters.

## Try it out

`npm install` and start a development server:

```bash
npm run dev
```

and navigate to http://localhost:5173
