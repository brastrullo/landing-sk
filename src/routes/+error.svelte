<script>
  import { page } from '$app/stores';
</script>

<h1>{$page.error?.message || `404 main` }</h1>