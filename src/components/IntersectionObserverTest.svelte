<script>
  import IntersectionObserver from "svelte-intersection-observer";

  let element;
  let intersecting;
  const handleObserver = (e) => {
    console.dir(e.detail); // IntersectionObserverEntry
    console.log(e.detail.isIntersecting); // true | false
  }
</script>

<section id="io" class="h-screen flex justify-center items-center z-40">
  <p class:intersecting class="bg-slate-400">
    {intersecting ? "Element is in view" : "Element is not in view"}
  </p>
  
  <IntersectionObserver {element} bind:intersecting on:observe={handleObserver}>
    <div bind:this={element}>Hello world</div>
  </IntersectionObserver>
</section>