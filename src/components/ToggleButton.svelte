<script>
	import { darkMode, toggleState } from '../utils/store'
	import Sun from '../svg/sun.svelte'
	import Moon from '../svg/moon.svelte'

	export let classNames = ''
</script>

<div class="flex items-center mr-2 ml-6">
	<label class="relative inline-block w-8 h-4">
		{#if $darkMode}
			<Moon classNames="-ml-5" />
		{:else}
			<Sun classNames="-ml-5" />
		{/if}
		<input on:click={toggleState} type="checkbox" class="opacity-0 w-0 h-0 bg-white" />
		<span
			class={`rounded-full absolute cursor-pointer top-0 left-0 right-0 bottom-0 bg-white border border-black dark:border-white transition ${classNames}`}
		/>
		<p class="sr-only">Dark Mode</p>
	</label>
</div>

<style lang="postcss">
	.icon:before {
		content: '';
	}
	label span:before {
		content: '';
		background: black;
		@apply absolute w-3 h-3 left-px bottom-px border border-black transition rounded-full;
	}

	input:checked + span {
		background-color: black;
	}

	input:focus + span {
		box-shadow: 0 0 1px rgb(82, 82, 82);
	}

	input:checked + span:before {
		background: white;
		@apply transform translate-x-4;
	}
</style>
