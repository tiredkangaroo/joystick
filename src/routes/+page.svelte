<!-- gray 1: #3d4046 -->
<!-- red 1: #fc2526 -->
<script lang="ts">
  import { onMount } from "svelte";

  let canvas: HTMLCanvasElement;
  onMount(() => {
    const ctx = canvas.getContext("2d");
    if (!ctx) return;

    canvas.width = canvas.offsetWidth;
    canvas.height = canvas.offsetHeight;

    var img = new Image();
    img.onload = () => {
      ctx.drawImage(img, 20, 20, 350, 350);
    };
    img.src = "/images/arcademachine.png";
  });
</script>

<canvas class="w-full h-full absolute" id="bgCanvas" bind:this={canvas}></canvas>
<main class="w-full h-full bg-[#050c2e]" id="bg">
  <!-- <header class="w-full h-16 flex flex-row justify-end items-center pr-4 absolute z-20">
    <button
      class="bg-[#ffe5e8] text-[#ec3750] hover:text-white border-2 border-[#ec3750] hover:bg-[#ec3750] duration-300 px-4 py-2 rounded-full"
    >
      Sign In
    </button>
  </header> -->
  <div class="absolute flex flex-col gap-2 z-10 w-full">
    <h1 class="text-[6rem]! text-center mt-[7%] gap-0" id="title">
      <span>j</span>
      <span>o</span>
      <span>y</span>
      <span>s</span>
      <span>t</span>
      <span>i</span>
      <span>c</span>
      <span>k</span>
    </h1>
    <p class="text-center text-2xl">make a game, get an <b class="text-3xl">arcade machine</b>!</p>
    <p class="text-center text-2xl">beginners always welcome!</p>
    <div class="flex flex-row justify-center mt-2">
      <button
        class="bg-[#f2f9ff] border-2 border-[#338eda] text-[#338eda] hover:bg-[#338eda] hover:text-white duration-300 w-fit px-4 py-2 rounded-full"
        >requirements</button
      >
    </div>
  </div>
</main>
