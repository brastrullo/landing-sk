<script>
	import { fade } from 'svelte/transition'
	export let title = ''
</script>

<h1
	in:fade
	out:fade={{ duration: 150 }}
	class="z-40 absolute rotate-90 origin-top-left top-10 -left-1 sm:left-0 text-8xl translate-x-[5.25rem] text-black/40 sm:text-black dark:text-white/40"
>
	{title}
</h1>
