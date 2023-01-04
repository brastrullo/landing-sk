<script>
	import LoadCalendly from './LoadCalendly.svelte'
	export let classNames = ''
	export let wrapperClassNames = 'my-[1.35rem] sm:my-0'
	export let text = 'contact'
</script>

<LoadCalendly
	{text}
	{wrapperClassNames}
	classNames={classNames}
/>
