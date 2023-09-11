<script>
	export let text
	export let classNames = ''
	export let wrapperClassNames = 'my-3'
	const calendlyHandler = (e) => {
		e.preventDefault()
		let urlObj = { url: 'https://calendly.com/rastr-studio/meet-brad' }
		// @ts-ignore
		Calendly.initPopupWidget(urlObj)
		return false
	}
</script>

<div class={`${wrapperClassNames}`}>
	<link href="https://assets.calendly.com/assets/external/widget.css" rel="stylesheet" />
	<script
		src="https://assets.calendly.com/assets/external/widget.js"
		type="text/javascript"
		async
	></script>
	<!-- svelte-ignore a11y-invalid-attribute -->
	<button class={`${classNames}`} on:click={calendlyHandler}>{text}</button>
</div>
