<script>
import { fly, fade } from 'svelte/transition';
import { quintInOut } from 'svelte/easing';
</script>
<h1 in:fade out:fade={{duration: 150}} class="absolute rotate-90 origin-top-left top-10 left-0 text-8xl translate-x-[5.25rem] z-40">CLIENTS</h1>
<div class="h-screen w-screen absolute top-0 left-0">
  <section class="flex flex-col justify-end sm:justify-center md:justify-start items-center h-screen">
    <div class="group relative transition">
      <img in:fly={{y: -1000, duration: 400, easing: quintInOut}} out:fade src="https://via.placeholder.com/3200x2000.png?text=marketing+image" alt="marketing" loading="lazy" class="bg-cover object-cover sm:w-[calc(100vw-4rem)] lg:w-[calc(75vw)] w-[calc(100vw-4rem)] h-[calc(100vh-4rem)] sm:h-auto mb-8 sm:mb-0 md:mt-12 lg:max-h-[70vh]"/>
      <a in:fly={{delay:250}} out:fade rel="noreferrer" href="https://bradleyrastrullo.com" target="_blank" class="opacity-20 group-hover:opacity-100 transition hover:scale-110 text-white px-10 py-4 font-semibold  absolute bottom-[85vh] sm:bottom-4 left-1/2 -translate-x-1/2 bg-black/40 hover:bg-black/20 hover:text-white/80">visit</a>
    </div>
    <p in:fly={{y: 1000, duration: 400, easing: quintInOut}} out:fade class="w-[calc(100vw-8rem)] md:w-[60vw] sm:my-4 max-h-[calc(70vh)] mb-14 sm:w-[calc(100vw-4rem)] text-center absolute sm:static overflow-auto first-letter:text-5xl first-letter:font-black">Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.</p>
  </section>
</div>