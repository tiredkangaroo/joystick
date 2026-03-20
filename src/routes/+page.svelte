<!-- gray 1: #3d4046 -->
<!-- red 1: #fc2526 -->
<script lang="ts">
  import { onMount } from "svelte";

  var selectedButton = $state(0);

  let canvas: HTMLCanvasElement;
  onMount(() => {
    const ctx = canvas.getContext("2d");
    if (!ctx) return;

    var selectedButton = $state(0);

    canvas.width = canvas.offsetWidth;
    canvas.height = canvas.offsetHeight;

    var img = new Image();
    img.onload = () => {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.save();
      ctx.translate(canvas.width / 5, canvas.height / 1.67);
      ctx.rotate((Math.PI / 180) * 15);
      ctx.drawImage(img, 20, 20, -img.width / 1.3, -img.height / 1.3);
      ctx.restore();
    };
    img.src = "/images/arcademachine.png";
  });

  document.onkeydown = (e) => {
    console.log(e.key);
    if (e.key === "ArrowDown") {
      if (selectedButton >= 1) {
        selectedButton = 0;
        return;
      }
      selectedButton++;
      console.log("selected button is,", selectedButton);
    } else if (e.key === "ArrowUp") {
      if (selectedButton <= 0) {
        selectedButton = 0;
        return;
      }
      selectedButton--;
    }
  };
  console.log("changed selected button to, ", selectedButton);
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
    <div class="flex flex-col items-center justify-center mt-8 gap-3">
      <button class="bg-[#f2f9ff] border-[#338eda] text-[#338eda] hover:bg-[#338eda]">
        {#if selectedButton === 0}
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="lucide lucide-chevron-right-icon lucide-chevron-right"
          >
            <path d="m9 18 6-6-6-6" />
          </svg>
        {/if}
        requirements</button
      >
      <button class="bg-[#ffe4e8] border-[#ec3750] text-[#ec3750] hover:bg-[#ec3750]">
        {#if selectedButton === 1}
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="lucide lucide-chevron-right-icon lucide-chevron-right"
          >
            <path d="m9 18 6-6-6-6" />
          </svg>
        {/if}
        sign in to hack club
      </button>
    </div>
  </div>
</main>
