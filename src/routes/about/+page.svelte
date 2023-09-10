<script>
	import ContactButton from '../../components/ContactButton.svelte'
	import { fly, fade } from 'svelte/transition'
	import { quintInOut } from 'svelte/easing'
	import AbsoluteScrollText from '../../components/AbsoluteScrollText.svelte'
	import VerticalTitleHeader from '../../components/VerticalTitleHeader.svelte'

	const imgSrc = "https://picsum.photos/seed/picsum/2000/1200.webp?w=1&p=1&blur=10"
	const lqoipSrc = "https://picsum.photos/seed/picsum/2000/1200.webp?w=1&p=1&blur=10&lqip"

	const title = 'ABOUT'

	const links = [
		{ name: 'github', url: 'https://github.com/brastrullo' },
		{ name: 'linkedin', url: 'https://linkedin.com/in/bradleyrastrullo' }
	]

	const mainText =
		'Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata'
</script>

<VerticalTitleHeader title={title} />
<div class="h-[calc(100vh-3.5rem)] w-screen relative top-0 left-0 z-0">
	<section
		class="md:ml-20 mx-4 sm:mt-14 mt-8 sm:pb-20 md:pb-0 flex flex-col sm:flex-row sm:items-end sm:flex-wrap md:flex-nowrap justify-end sm:justify-start"
	>
		<article
			class="md:mr-4 sm:ml-0 sm:w-full lg:max-w-[30vw] mb-4 flex flex-col h-full sm:flex-col-reverse md:flex-col"
		>
			<div
				class="links flex justify-center md:justify-end mb-1 font-thin"
				in:fly={{ x: -300, delay: 150, duration: 500 }}
				out:fade
			>
				{#each links as link}
					<a
						rel="noreferrer"
						href={link.url}
						target="_blank"
						class="hover:underline underline-offset-4 font-light">{link.name}</a
					>
					{#if link !== links[links.length - 1]}
						<span class="mx-2">|</span>
					{/if}
				{/each}
			</div>
			<img
				in:fly={{ x: -1000, easing: quintInOut, duration: 650 }}
				out:fade
				src={lqoipSrc}
				data-src={imgSrc}
				class="bg-cover object-cover bg-gray-200 h-[calc(100vh-5rem)] sm:h-[calc(100vh-6.5rem)] w-full"
				loading="lazy"
				alt="Profile"
			/>
		</article>
		<div
			class="absolute sm:static sm:flex sm:flex-col-reverse md:flex-col w-[calc(100%-2rem)] sm:w-auto mb-8 sm:mb-4"
		>
			<div
				class="fade-text-wrapper relative flex flex-col justify-end sm:static bottom-0 sm:bg-none bg-gradient-to-b from-transparent via-neutral-400/90 neutral-400"
			>
				<p
					class="fade-text overflow-scroll md:max-w-[30rem] inline-block h-[80vh] sm:h-min max-h-[20rem] sm:max-h-[30rem] px-6 pt-20 pb-20 sm:p-0 sm:max-h-auto sm:mt-0 sm:mb-8 first-letter:text-5xl first-letter:font-black md:first-letter:text-9xl md:first-letter:font-bold"
					in:fly={{ y: 1000, easing: quintInOut, duration: 550 }}
					out:fade
				>
					{mainText}
				</p>
				<AbsoluteScrollText />
			</div>
			<div
				in:fly={{ delay: 150, y: 300, easing: quintInOut, duration: 550 }}
				out:fade
				class="flex justify-center md:justify-start"
			>
				<ContactButton classNames="font-bold transition drop-shadow text-base border border-transparent text-white py-6 px-[calc(50vw-4rem)] sm:px-20 bg-black/30 dark:bg-white/30 sm:bg-black hover:bg-white/30 dark:hover:bg-black/50 hover:text-black/50 dark:hover:text-white/80 sm:hover:text-black sm:hover:bg-transparent sm:hover:border-black z-50" />
			</div>
		</div>
	</section>
	</div>

<style lang="postcss">
	@media (max-width: 640px) {
		.fade-text {
			-webkit-mask-image: linear-gradient(
				to bottom,
				transparent 0%,
				white 25%,
				white 75%,
				transparent 100%
			);
			mask-image: linear-gradient(
				to bottom,
				transparent 0%,
				white 25%,
				white 75%,
				transparent 100%
			);
		}
	}
</style>
