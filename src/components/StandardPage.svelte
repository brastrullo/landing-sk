<script>
	import { fly, fade } from 'svelte/transition'
	import { quintInOut } from 'svelte/easing'
	import VerticalTitleHeader from '../components/VerticalTitleHeader.svelte'
  
  export let title
  export let src
  export let href
  export let mainText
  export let subText
</script>

<VerticalTitleHeader {title} />
<div class="h-screen w-screen absolute top-0 left-0">
  <section
    class="flex flex-col justify-end sm:justify-center md:justify-start items-center h-screen"
  >
    <div class="relative transition">
      <img
        in:fly={{ y: -1000, duration: 400, easing: quintInOut }}
        out:fade
        {src}
        width="3200"
        height="2000"
        alt={title}
        loading="lazy"
        class="bg-cover bg-gray-200 object-cover sm:w-[calc(100vw-10rem)] lg:w-[calc(75vw)] w-[calc(100vw-4rem)] h-[calc(100vh-4rem)] sm:h-[60vh] md:h-auto mb-8 sm:mb-0 md:mt-12 lg:max-h-[70vh]"
      />
      <a
        in:fly={{ delay: 250 }}
        out:fade
        rel="noreferrer"
        {href}
        target="_blank"
        class="transition hover:scale-110 text-white px-10 py-4 font-semibold  absolute bottom-[80vh] sm:bottom-4 left-1/2 -translate-x-1/2 bg-black/40 hover:bg-black/40 hover:text-white/80"
        >visit</a
      >
    </div>
    <p
      in:fly={{ y: 1000, duration: 400, easing: quintInOut }}
      out:fade
      class="w-[calc(100vw)] px-8 pb-4 sm:p-0 md:w-[60vw] sm:my-4 max-h-[calc(70vh)] mb-14 sm:w-[calc(100vw-4rem)] text-center absolute sm:static first-letter:text-5xl first-letter:font-black bg-gradient-to-b from-transparent via-white/70 dark:via-black md:bg-none"
    >
      {mainText}
      <span class="block mt-2">{subText}</span>
    </p>
  </section>
</div>