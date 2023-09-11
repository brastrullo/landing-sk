<script>
	import '../app.css'
	import { browser } from '$app/environment'
	import { page } from '$app/stores'
	import { fly, fade, slide } from 'svelte/transition'
	import { quintInOut } from 'svelte/easing'
	import ToggleButton from '../components/ToggleButton.svelte'
	import ContactButtonSmall from '../components/ContactButtonSmall.svelte'
	import { writable, get } from 'svelte/store'
	import { darkMode } from '../utils/store'
	
	const modalIsOpen = writable(false)

	const isDarkMode = get(darkMode)

	const links = [
		{ name: 'home', href: '/' },
		{ name: 'about', href: '/about' },
		{ name: 'clients', href: '/clients' },
		{ name: 'blog', href: '/blog' },
		{ name: 'social', href: '/social' }
	]

	$: isHome = $page.url.pathname === '/'
	$: isAbout = $page.url.pathname === '/about'
	// $: isClients = $page.url.pathname === '/clients'
	// $: isBlog = $page.url.pathname === '/blog'
	// $: isSocial = $page.url.pathname === '/social'

	$: shouldBeHidden = isHome
	$: hideContactButton = isAbout || isHome

	const toggleModal = () => {
		modalIsOpen.update((n) => !n)
		if (browser) {
			document.querySelector('body')?.classList.toggle('overflow-hidden')
		}
	}
</script>

<header class="relative">
	<nav>
		<ul
			class="w-full flex justify-between h-6 sm:h-12 fixed top-0 left-0 z-50 bg-gradient-to-b from-white dark:from-black via-white/90  dark:via-black/90 items-center"
		>
			<li>
				<a href="/" class="ml-2 sm:ml-4 w-2/3 font-extralight dark:text-white">bradleyrastru||o</a>
			</li>
			<li class="w-1/3 flex justify-end">
				{#if !$modalIsOpen}
					<a
						href="/about"
						class="md:hidden mr-8 font-semibold"
						style={`${isAbout ? 'display:none' : ''}`}>about</a
					>
					<button class="md:hidden mr-4 font-semibold" on:click={toggleModal}>menu</button>
				{/if}
				<ul class="hidden md:flex justify-end items-center">
					<li class:hidden={hideContactButton} class="mr-6"><ContactButtonSmall /></li>
					<li class="mr-4 hover:underline underline-offset-4 font-semibold">
						<a href="/about">about</a>
					</li>
					<li>
						<ToggleButton />
					</li>
				</ul>
			</li>
		</ul>
		<ul
			in:fly={{ y: 100, duration: 250, easing: quintInOut }}
			style={`${shouldBeHidden ? 'display:none' : ''}`}
			class="hidden font-light md:flex fixed rotate-90 w-[40vh] justify-end translate-x-0 -translate-y-[40vh] bottom-0 origin-bottom-left z-50"
		>
			{#each links.slice(2) as link, i}
				<li class="transition mr-12 hover:scale-110 hover:drop-shadow-sm">
					<a href={link.href} class:line-through={$page.url.pathname === `/${link.name}`}
						>{link.name.toUpperCase()}</a
					>
				</li>
			{/each}
		</ul>
	</nav>
</header>

{#if $modalIsOpen}
	<div class="bg-black/70 fixed h-screen w-screen top-0 left-0 z-[60] flex flex-col">
		<div
			transition:fly={{ easing: quintInOut, y: -150, duration: 250 }}
			class="dark:bg-black bg-white flex justify-between border-b border-black/10 dark:border-white/10 h-[4rem]"
		>
			<ToggleButton />
			<a href="/" on:click={toggleModal} class="my-auto ml-4 font-light">bradleyrastru||o</a>
			<button
				on:click={toggleModal}
				class="text-black z-[80] m-4 font-black text-3xl dark:text-white">X</button
			>
		</div>
		<ul class="w-screen flex flex-col text-center text-2xl font-bold">
			{#each links as link, i}
				<li
					transition:fly={{
						easing: quintInOut,
						x: i % 2 === 0 ? 400 : -400,
						duration: 425 - i * 5
					}}
					class={`h-[calc(100vh/5-.5rem)] flex border-b border-black/10 bg-white dark:border-white/10 dark:bg-black`}
				>
					<a
						class="transition hover:scale-125 py-14 px-[calc(30vw-1rem)] m-auto"
						href={link.href}
						on:click={toggleModal}>{link.name}</a
					>
				</li>
			{/each}
		</ul>
	</div>
{/if}

<slot />
