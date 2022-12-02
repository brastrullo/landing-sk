<script>
  import "../app.css"
  import { browser } from '$app/environment';
  import { page } from "$app/stores"
  import { fly, fade, slide } from 'svelte/transition';
  import { quintInOut } from 'svelte/easing';
  import ToggleButton from "../components/ToggleButton.svelte";
  import LoadCalendly from "../components/LoadCalendly.svelte";
  import { writable } from 'svelte/store';

  const modalIsOpen = writable(false);

  $: isHome = $page.url.pathname === '/';
  $: isClients = $page.url.pathname === '/clients';
  $: isAbout = $page.url.pathname === '/about';
  $: isBlog = $page.url.pathname === '/blog';
  $: isSocial = $page.url.pathname === '/social';

  $: shouldBeHidden = isHome;
  $: hideContactButton = isAbout || isHome;

  modalIsOpen.subscribe(value => {
    console.log(value);
  });

  const toggleModal = () => {
    modalIsOpen.update(n => !n);
    if (browser) {
      document.querySelector('body')?.classList.toggle('overflow-hidden');
    }
  }
</script>

<header class="relative">
  <nav>
    <ul class="w-full flex justify-between h-6 sm:h-12 fixed top-0 left-0 z-50 bg-gradient-to-b from-white via-white/90 items-center">
      <li><a href="/" class="ml-2 sm:ml-4 w-2/3 font-extralight">bradleyrastru||o</a></li>
      <li class="w-1/3 flex justify-end">
        {#if !$modalIsOpen}
          <a href="/about" class="md:hidden mr-8 font-semibold" style={`${isAbout ? 'display:none': ''}`}>about</a>
          <button class="md:hidden mr-4 font-semibold" on:click={toggleModal}>menu</button>
        {/if}
        <ul class="hidden md:flex justify-end items-center">
          <li class:hidden={hideContactButton} class="mr-6"><LoadCalendly text=contact classNames="transition drop-shadow-sm home-cta text-sm font-semibold border border-transparent py-1 px-4 bg-black text-white hover:text-black hover:bg-transparent hover:border-black"/></li>
          <li class="mr-4 hover:underline underline-offset-4 font-semibold"><a href="/about">about</a></li>
          <li class="ml-6">
            <ToggleButton />
          </li>
        </ul>
      </li>
    </ul>
    <ul in:fly={{y:100, duration: 250, easing: quintInOut}} style={`${shouldBeHidden ? 'display:none': ''}`} class="hidden font-light md:flex fixed rotate-90 w-[40vh] justify-end translate-x-0 -translate-y-[40vh] bottom-0 origin-bottom-left z-50">
      <li class="transition mr-12 hover:scale-110 hover:drop-shadow-sm"><a href="/clients" class:line-through={isClients}>CLIENTS</a></li>
      <li class="transition mr-12 hover:scale-110 hover:drop-shadow-sm"><a href="/blog" class:line-through={isBlog}>BLOG</a></li>
      <li class="transition mr-4 hover:scale-110 hover:drop-shadow-sm"><a href="/social" class:line-through={isSocial}>SOCIAL</a></li>
    </ul>
  </nav>
</header>

{#if $modalIsOpen}
  <div class="bg-black/70 fixed h-screen w-screen top-0 left-0 z-[60] flex flex-col">
    <div transition:fly={{easing: quintInOut,y:-150, duration:250}} class="bg-white flex justify-between border-b border-black/10 h-[4rem]">
      <p class="my-auto ml-4 font-light">bradleyrastru||o</p>
      <button on:click={toggleModal} class="text-black z-[80] m-4 font-black text-3xl">X</button>
    </div>
    <ul class="w-screen flex flex-col text-center text-2xl font-bold">
      <li transition:fly={{easing: quintInOut,x:-400, duration:425}} class="h-[calc(100vh/4-1rem)] flex border-b border-black/10 bg-white"><a class="transition hover:scale-125 py-14 px-[calc(30vw-1rem)] m-auto " href="/about" on:click={toggleModal}>about</a></li>
      <li transition:fly={{easing: quintInOut,x:400, duration:400, delay: 50}} class="h-[calc(100vh/4-1rem)] flex border-b border-black/10 bg-white"><a class="transition hover:scale-125 py-14 px-[calc(30vw-1rem)] m-auto " href="/clients" on:click={toggleModal}>clients</a></li>
      <li transition:fly={{easing: quintInOut, x:-400, duration:350, delay:100}} class="h-[calc(100vh/4-1rem)] flex border-b border-black/10 bg-white"><a class="transition hover:scale-125 py-14 px-[calc(30vw-1rem)] m-auto" href="/blog" on:click={toggleModal}>blog</a></li>
      <li transition:fly={{easing: quintInOut, x:400, duration:325, delay:150}} class="h-[calc(100vh/4-1rem)] flex bg-white"><a class="transition hover:scale-125 py-14 px-[calc(30vw-1rem)] m-auto" href="/social" on:click={toggleModal}>social</a></li>
    </ul>
  </div>  
{/if}

<slot/>