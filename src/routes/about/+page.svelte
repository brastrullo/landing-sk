<script>
import LoadCalendly from "../../components/LoadCalendly.svelte"
import { fly, slide, fade } from 'svelte/transition';
import { quintInOut } from 'svelte/easing';

</script>
<h1 in:fade out:fade={{duration: 150}} class="absolute rotate-90 origin-top-left top-10 left-0 text-8xl translate-x-[5.25rem] z-40 text-black/70 md:text-black">ABOUT</h1>
<div class="h-[calc(100vh-3.5rem)] w-screen relative top-0 left-0 z-0">
  <section class="md:ml-20 mx-4 sm:mt-14 mt-8 sm:pb-20 md:pb-0 flex flex-col sm:flex-row sm:items-end sm:flex-wrap md:flex-nowrap justify-end sm:justify-start">
    <article class="md:mr-4 sm:ml-0 sm:w-full lg:max-w-[30vw] mb-4 flex flex-col h-full sm:flex-col-reverse md:flex-col">
      <div class="flex justify-center md:justify-end mb-1 font-thin" in:fly={{x: -300, delay: 150, duration:500}} out:fade>
        <a href="https://github.com/brastrullo" target="_blank" class="mr-2 hover:underline underline-offset-4 font-light">github</a>
        |
        <a href="https://linkedin.com/in/bradleyrastrullo" target="_blank" class="ml-2 hover:underline underline-offset-4 font-light">linkedin</a>
      </div>
      <img in:fly={{x: -1000, easing: quintInOut, duration: 650}} out:fade src="https://www.fillmurray.com/2000/1200" class="bg-cover object-cover h-[calc(100vh-5rem)] sm:h-[calc(100vh-6.5rem)] w-full" loading="lazy" alt="Profile" />
    </article>
    <div class="absolute sm:static sm:flex sm:flex-col-reverse md:flex-col w-[calc(100%-2rem)] sm:w-auto mb-8 sm:mb-4 bg-gradient-to-b from-transparent via-white">
      <p class="overflow-scroll md:max-w-[30rem] inline-block h-min max-h-[15rem] sm:max-h-[30rem] p-8 mb-4 sm:p-0 sm:m-0 sm:max-h-auto sm:my-8 first-letter:text-5xl first-letter:font-black md:first-letter:text-9xl md:first-letter:font-bold" in:fly={{y: 1000, easing: quintInOut, duration: 550}} out:fade>Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.
        Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata</p>
      <span class="-rotate-90 absolute bottom-1/2 right-6 translate-x-1/2 font-thin opacity-30 animate-pulse text-xs sm:hidden">scroll</span>
      <div in:fly={{delay: 150, y: 300, easing: quintInOut, duration: 550}} out:fade class="flex justify-center md:justify-start">
        <LoadCalendly text="contact" wrapperClassNames="my-[1.35rem]" classNames="font-bold transition drop-shadow text-base border border-transparent py-6 px-[calc(50vw-4rem)] sm:px-20 bg-black/20 sm:bg-black text-white hover:bg-white/20 hover:text-black/50 sm:hover:text-black sm:hover:bg-white  sm:hover:border-black z-50"/>
      </div>
    </div>
  </section>
</div>