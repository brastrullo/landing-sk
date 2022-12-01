<script>
import { browser } from '$app/environment';
import { onMount } from 'svelte';
import { slide, fade, fly } from 'svelte/transition';
import { quintInOut } from 'svelte/easing';
import LoadCalendly from '../components/LoadCalendly.svelte';
import Scene from '../components/Scene.svelte';

if (browser) {
  onMount(async () => {
    let options = {
      root: null,
      rootMargin: '0px',
      threshold: 1.0
    }
    
    let callback = (entries, observer) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          // const mainTextContainsHidden = !(document.querySelector('.home-main-text')?.classList.contains('hidden'));
          // const subTextContainsHidden = !(document.querySelector('.home-sub-text')?.classList.contains('hidden'));
          // if (mainTextContainsHidden) document.querySelector('.home-main-text')?.classList.add('hidden');
          // if (subTextContainsHidden) document.querySelector('.home-sub-text')?.classList.add('hidden');
        }
      });
    };
    
    const observer = new IntersectionObserver(callback, options);
    const target = document.querySelector('.items-scrolled');
    if (target && observer) {
      observer.observe(target);
    }
  });
}
</script>

<h1 class="hidden">Home</h1>
<Scene />
<div id="scrollArea" class="bg-transparent">
  <div class="return-home"/>
  <div class="sm:h-screen w-screen transition-opacity flex flex-col sm:flex-row justify-end sm:justify-between sm:items-end sm:p-20">
    <div class="h-screen sm:h-auto flex flex-col justify-end">
      <p class="z-40 home-main-text text-5xl sm:text-7xl sm:max-w-80 mx-4 md:max-w-[40rem] font-bold mb-8 sm:mb-0" in:fade out:fly={{y:300, duration: 250, easing: quintInOut}}>"I create UI, Motion Graphics and anything we can imagine.</p>
      <span class="z-40 sm:hidden text-center animate-bounce text-xs font-extralight opacity-60">scroll down</span>
    </div>
    <div class="h-screen sm:h-auto text-2xl flex flex-col justify-end sm:w-1/2 sm:bottom-20 sm:right-20 text-center sm:text-right mb-8 sm:mb-0">
      <p class="z-40 home-sub-text mb-[calc(25vh)] px-2 sm:px-0 sm:mb-4 sm:pl-4 font-light drop-shadow-2xl bg-gradient-to-b from-transparent via-white sm:bg-none" in:fade out:fly={{x:600, duration: 250, easing: quintInOut}}>A multi-disciplinary creative using JS & CSS</p>
      <div in:fade out:fly={{delay: 100, x:600, duration: 250, easing: quintInOut}} class="drop-shadow-2xl z-40">
        <LoadCalendly text=contact wrapperClassNames="my-[1.25rem]" classNames="transition home-cta text-base font-bold border border-transparent py-6 sm:py-6 px-[calc(50%-4rem)] sm:px-8 md:px-14 lg:px-20 bg-black text-white hover:text-black hover:bg-white hover:border-black"/>
      </div>
    </div>
  </div>
  <div class="hidden sm:flex h-screen w-screen items-end">
    <div class="items-scrolled z-50"/>
    <ul out:fly={{y: 600, duration: 500}} class="z-40 font-extralight text-4xl mx-auto py-6 flex w-[90vw] justify-around border border-l-0 border-r-0 border-solid border-neutral-300 mb-20">
      <li class="transition hover:scale-110 text-shadow"><a href="/clients" data-svelte-no-scroll>CLIENTS</a></li>
      <li class="transition hover:scale-110 text-shadow"><a href="/blog" data-svelte-no-scroll>BLOG</a></li>
      <li class="transition hover:scale-110 text-shadow"><a href="/social" data-svelte-no-scroll>SOCIAL</a></li>
    </ul>
  </div>
</div>


