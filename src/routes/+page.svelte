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
      ctx.translate(canvas.width / 20, canvas.height / 6);
      ctx.rotate((Math.PI / 180) * 15);
      ctx.drawImage(img, 0, 0);
      ctx.restore();
    };
    img.src = "/images/arcademachine.png";
  });

  const numButtons = 3;
  const buttonLink = ["#requirements", "#demos", "#faq"];
  document.onkeydown = (e) => {
    console.log(e.key);
    if (e.key === "ArrowDown") {
      if (selectedButton >= numButtons - 1) {
        selectedButton = 0;
        e.preventDefault();
        return;
      }
      selectedButton++;
    } else if (e.key === "ArrowUp") {
      if (selectedButton <= 0) {
        selectedButton = numButtons - 1;
        e.preventDefault();
        return;
      }
      selectedButton--;
    } else if (e.key === "Enter") {
      window.location.href = buttonLink[selectedButton];
    }
  };
</script>

<div class="absolute right-0 top-0 bg-white text-black z-30 flex flex-row gap-2 px-2 py-2">
  <input
    type="checkbox"
    onchange={(e) => {
      if ((e.target as HTMLInputElement).checked) {
        document.getElementsByTagName("html")[0].style.fontFamily = "Times New Roman, serif";
      } else {
        document.getElementsByTagName("html")[0].style.fontFamily = "Pixelify Sans, Times, serif";
      }
    }}
  />
  <p class="font-[Times_New_Roman,serif]">enable easier to read font</p>
</div>
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
    <div class="flex flex-col items-center justify-center mt-8 gap-3 w-full">
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
      <button class="bg-[#f2f9ff] border-[#24b971] text-[#24b971] hover:bg-[#24b971]">
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
        demos</button
      >
      <button class="bg-[#ffe4e8] border-[#ec3750] text-[#ec3750] hover:bg-[#ec3750]">
        {#if selectedButton === 2}
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
        faq
      </button>
      <p class="bg-white text-black px-2">use the up/down arrow keys to navigate. press enter to select.</p>
    </div>
  </div>
  <div class="z-30 absolute bottom-2 right-2 bg-black px-2 py-2">
    <p>made with ❤️ by <a href="https://hackclub.com" target="_blank" class="text-blue-200 underline">hack club</a></p>
    <div class="flex flex-row gap-2">
      <a href="https://github.com/tiredkangaroo/joystick" target="_blank" class="text-blue-200 underline"
        >open source!</a
      >
      |
      <a href="https://hackclub.com/slack" target="_blank" class="text-blue-200 underline">join the slack!</a>
    </div>
  </div>
</main>
<div class="bg-[#050c2e] w-full h-full" id="requirements">
  <h1 class="text-[12vw] text-center">requirements</h1>
  <div class="w-full items-center justify-center flex">
    <ol class="list-decimal list-inside text-2xl flex flex-col gap-12 items-start justify-center px-4">
      <li class="list-item text-red-300 font-[times_new_roman]">
        you must be <b class="">13-18 years old</b>. hack club is for teens!
      </li>
      <li class="list-item text-orange-300">
        your game must be original. avoid copying existing games. <br />
        <span class="text-white text-lg font-[times_new_roman]"
          >we want to see your creativity shine! if your game is similar to an existing game, make sure to add your own
          unique twist.</span
        >
      </li>
      <li class="list-item text-yellow-300">
        your game should be fun and engaging!<br />
        <span class="text-white text-lg font-[times_new_roman]">aim for five minutes of engaging gameplay.</span>
      </li>
      <li class="list-item text-green-400">
        absolutely NO ai generated art or music. <br />
        <span class="text-white text-lg font-[times_new_roman]"
          >additionally, minimize the use of ai in code. we want to see your creativity, even if it's not perfect!</span
        >
      </li>
      <li class="list-item text-blue-400">
        your game must be playable on a computer or mobile device.<br />
        <span class="text-white text-lg font-[times_new_roman]">
          building your game to the web will ensure it's accessible to as many people and will speed up the review
          process.
        </span>
      </li>
      <li class="list-item text-purple-400">
        you must log your time using hackatime and lapse. <br />
        <span class="font-[times_new_roman] text-white text-lg">
          check out <a href="https://hackatime.hackclub.com" target="_blank" class="text-blue-200 underline"
            >hackatime</a
          >
          and <a href="https://lapse.hackclub.com" target="_blank" class="text-blue-200 underline">lapse</a>.
        </span>
      </li>
    </ol>
  </div>
</div>
