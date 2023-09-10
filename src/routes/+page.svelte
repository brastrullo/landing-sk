<script>
	import { fade, fly } from 'svelte/transition'
	import { quintInOut } from 'svelte/easing'
	import ContactButton from '../components/ContactButton.svelte'
	import Scene from '../components/Scene.svelte'
	// import SceneOld from '../components/SceneOld.svelte'
	// import IntersectionObserverTest from '../components/IntersectionObserverTest.svelte'
	// import IntersectionObserverTest2 from '../components/IntersectionObserverTest2.svelte'
	// import IntersectionObserver from 'svelte-intersection-observer'

	let windowHeight = 0
	let windowWidth = 0
	let buttonWidth = 0
	let buttonOffsetWidth = 0
	let buttonMidPos = 0
	let element1
	let scrollY = 0

	const navItems = ['clients', 'blog', 'social']
	const handleObserver = (e) => {
		if (e.detail.isIntersecting) {
			console.log('observe', e.detail.intersectionRatio)
		}
	}
	const handleIntersect = (e) => {
		if (e.detail.isIntersecting) {
			console.log('intersect', e.detail.intersectionRatio)
		}
	}
	// $: buttonMidPos = (windowWidth / 2) 
	// $: console.log({windowHeight, windowWidth, buttonMidPos, scrollY})

	// const styledAnimation = `transform: translate(-${scrollY >= windowHeight * .3 ? buttonMidPos : scrollY * 0.3 * 10}px, ${scrollY}px);`
	// const styledAnimation2 = `transform: translate(-${scrollY * 0.3 * 10 > 400 ? 400 : scrollY * 0.3 * 10}px, ${scrollY}px); opacity: ${10/ scrollY};`
</script>

<svelte:window bind:scrollY bind:innerHeight={windowHeight} bind:innerWidth={windowWidth}/>
<h1 class="hidden">Home</h1>
<div class="w-screen h-screen p-10 fixed top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">
	<Scene {scrollY} />
</div>
<div id="scrollArea" class="bg-transparent">
	<div class="return-home" />
		<div
			class="sm:h-screen w-screen transition-opacity flex flex-col sm:flex-row justify-end sm:justify-between sm:items-end sm:p-20"
		>
			<div class="h-screen sm:h-auto flex flex-col justify-end">
				<p
					style={`transform: translate(-${scrollY * 0.7 * 10}px, ${scrollY}px); opacity: ${
						10 / scrollY
					};`}
					bind:this={element1}
					class={`${scrollY > 75 ? 'invisible':''} z-40 home-main-text text-5xl sm:text-7xl sm:max-w-80 mx-4 md:max-w-[40rem] font-bold mb-8 sm:mb-0`}
					in:fade
					out:fly={{ y: 300, duration: 250, easing: quintInOut }}
				>
					"I create UI, Motion Graphics and anything we can imagine.
				</p>
				<span
					style={`transform: translate(0px, ${scrollY}px); opacity: ${
						10 / scrollY
					};`}
					class={`${scrollY > 25 ? 'invisible' : ''} animate-bounce sm:visible z-40 pb-1 sm:hidden text-center text-xs font-extralight opacity-60`}
					>scroll down</span
				>
			</div>
			<div
				style={`${windowWidth > 640 ? `transform: translate(${scrollY * 0.7 * 10}px, ${scrollY}px); opacity: ${
					10 / scrollY
				};` : ''}`}
				class={`${scrollY > 25 ? 'sm:invisible' : ''} sm:visible h-screen sm:h-auto text-2xl flex flex-col justify-end sm:w-1/2 sm:bottom-20 sm:right-20 text-center sm:text-right mb-8 sm:mb-0`}
			>
				<p
					class="z-40 home-sub-text mb-[calc(25vh)] px-2 sm:px-0 sm:mb-4 sm:pl-4 font-light drop-shadow-2xl bg-gradient-to-b from-transparent via-white/70 sm:bg-none dark:via-black/70"
					in:fade
					out:fly={{ x: 600, duration: 250, easing: quintInOut }}
				>
					A multi-disciplinary creative using JS & CSS
				</p>
				<!-- bind:clientWidth={buttonWidth}
				bind:offsetWidth={buttonOffsetWidth} -->
				<div
					in:fade
					out:fly={{ delay: 100, x: 600, duration: 250, easing: quintInOut }}
					class="drop-shadow-2xl z-40"
				>
					<ContactButton
						wrapperClassNames="my-[1.25rem]"
						classNames="home-cta font-bold transition drop-shadow text-base border border-transparent py-6 sm:py-6 px-[calc(50%-4rem)] sm:px-8 md:px-14 lg:px-20 bg-black text-white dark:bg-white/95 dark:text-black hover:text-black hover:bg-transparent hover:border-black dark:hover:text-white dark:hover:bg-black dark:hover:border-white"
					/>
				</div>
			</div>
		</div>
	<div class="hidden sm:flex h-screen w-screen items-end">
		<div class="z-50" />
		<ul
			out:fly={{ y: 600, duration: 500 }}
			class="z-40 font-extralight text-4xl mx-auto py-6 flex w-[90vw] justify-around border border-l-0 border-r-0 border-solid border-neutral-300 mb-20"
		>
			{#each navItems as item}
				<li class="transition hover:scale-110 text-shadow">
					<a href={`/${item}`} data-svelte-no-scroll>{item.toUpperCase()}</a>
				</li>
			{/each}
		</ul>
	</div>
</div>
