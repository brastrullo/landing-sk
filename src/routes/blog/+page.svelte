<script>
	import { page } from '$app/stores';
	import StandardPage from '../../components/StandardPage.svelte'
</script>

{#key $page.url}
	<StandardPage title={$page.data.title} src={$page.data.imgSrc} href={$page.data.href} mainText={$page.data.mainText} subText={$page.data.subText} />
	<slot></slot>
{/key}