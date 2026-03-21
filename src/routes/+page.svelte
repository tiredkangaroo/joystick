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

    function drawImage(ctx: CanvasRenderingContext2D, i: HTMLImageElement) {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.save();
      ctx.translate(canvas.width / 20, canvas.height / 6);
      ctx.rotate((Math.PI / 180) * 15);
      ctx.drawImage(i, 0, 0);
      ctx.restore();
    }
    var img = new Image();
    img.src = "/images/arcademachine.png";
    img.onload = () => {
      drawImage(ctx, img);
    };
    window.onresize = () => {
      canvas.width = canvas.offsetWidth;
      canvas.height = canvas.offsetHeight;
      drawImage(ctx, img);
    };
  });

  const numButtons = 2;
  const buttonLink = ["#how-works", "#requirements"];
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

  // https://stackoverflow.com/a/11381730/16467184
  function mobileCheck() {
    let check = false;
    (function (a) {
      if (
        /(android|bb\d+|meego).+mobile|avantgo|bada\/|blackberry|blazer|compal|elaine|fennec|hiptop|iemobile|ip(hone|od)|iris|kindle|lge |maemo|midp|mmp|mobile.+firefox|netfront|opera m(ob|in)i|palm( os)?|phone|p(ixi|re)\/|plucker|pocket|psp|series(4|6)0|symbian|treo|up\.(browser|link)|vodafone|wap|windows ce|xda|xiino/i.test(
          a,
        ) ||
        /1207|6310|6590|3gso|4thp|50[1-6]i|770s|802s|a wa|abac|ac(er|oo|s\-)|ai(ko|rn)|al(av|ca|co)|amoi|an(ex|ny|yw)|aptu|ar(ch|go)|as(te|us)|attw|au(di|\-m|r |s )|avan|be(ck|ll|nq)|bi(lb|rd)|bl(ac|az)|br(e|v)w|bumb|bw\-(n|u)|c55\/|capi|ccwa|cdm\-|cell|chtm|cldc|cmd\-|co(mp|nd)|craw|da(it|ll|ng)|dbte|dc\-s|devi|dica|dmob|do(c|p)o|ds(12|\-d)|el(49|ai)|em(l2|ul)|er(ic|k0)|esl8|ez([4-7]0|os|wa|ze)|fetc|fly(\-|_)|g1 u|g560|gene|gf\-5|g\-mo|go(\.w|od)|gr(ad|un)|haie|hcit|hd\-(m|p|t)|hei\-|hi(pt|ta)|hp( i|ip)|hs\-c|ht(c(\-| |_|a|g|p|s|t)|tp)|hu(aw|tc)|i\-(20|go|ma)|i230|iac( |\-|\/)|ibro|idea|ig01|ikom|im1k|inno|ipaq|iris|ja(t|v)a|jbro|jemu|jigs|kddi|keji|kgt( |\/)|klon|kpt |kwc\-|kyo(c|k)|le(no|xi)|lg( g|\/(k|l|u)|50|54|\-[a-w])|libw|lynx|m1\-w|m3ga|m50\/|ma(te|ui|xo)|mc(01|21|ca)|m\-cr|me(rc|ri)|mi(o8|oa|ts)|mmef|mo(01|02|bi|de|do|t(\-| |o|v)|zz)|mt(50|p1|v )|mwbp|mywa|n10[0-2]|n20[2-3]|n30(0|2)|n50(0|2|5)|n7(0(0|1)|10)|ne((c|m)\-|on|tf|wf|wg|wt)|nok(6|i)|nzph|o2im|op(ti|wv)|oran|owg1|p800|pan(a|d|t)|pdxg|pg(13|\-([1-8]|c))|phil|pire|pl(ay|uc)|pn\-2|po(ck|rt|se)|prox|psio|pt\-g|qa\-a|qc(07|12|21|32|60|\-[2-7]|i\-)|qtek|r380|r600|raks|rim9|ro(ve|zo)|s55\/|sa(ge|ma|mm|ms|ny|va)|sc(01|h\-|oo|p\-)|sdk\/|se(c(\-|0|1)|47|mc|nd|ri)|sgh\-|shar|sie(\-|m)|sk\-0|sl(45|id)|sm(al|ar|b3|it|t5)|so(ft|ny)|sp(01|h\-|v\-|v )|sy(01|mb)|t2(18|50)|t6(00|10|18)|ta(gt|lk)|tcl\-|tdg\-|tel(i|m)|tim\-|t\-mo|to(pl|sh)|ts(70|m\-|m3|m5)|tx\-9|up(\.b|g1|si)|utst|v400|v750|veri|vi(rg|te)|vk(40|5[0-3]|\-v)|vm40|voda|vulc|vx(52|53|60|61|70|80|81|83|85|98)|w3c(\-| )|webc|whit|wi(g |nc|nw)|wmlb|wonu|x700|yas\-|your|zeto|zte\-/i.test(
          a.substr(0, 4),
        )
      )
        check = true;
    })(navigator.userAgent || navigator.vendor || window.opera);
    return check;
  }
</script>

<div class="absolute right-0 top-0 bg-white text-black z-30 flex flex-row gap-2 px-2 py-2 text-sm md:text-bas">
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
    <h1 class="lg:text-[14vw] md:text-[18vw] text-[20vw] text-center lg:mt-[3%] md:mt-[15%] mt-[30%] gap-0" id="title">
      <span>j</span>
      <span>o</span>
      <span>y</span>
      <span>s</span>
      <span>t</span>
      <span>i</span>
      <span>c</span>
      <span>k</span>
    </h1>
    <div class="text-center w-full flex flex-row justify-center">
      <p class="text-[clamp(1.5rem,3vw,2rem)] bg-[#050c2e] w-fit">
        make a game, get an <b class="text-[clamp(1.1rem,3vw,1.875rem)]">arcade machine</b>!
      </p>
    </div>
    <div class="flex flex-col items-center justify-center mt-8 gap-3 w-full">
      <button
        class="bg-[#fff2f2] border-[#b92424] text-[#b92424] hover:bg-[#b92424]"
        onclick={() => {
          window.location.href = buttonLink[0];
        }}
      >
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
        how does this work?</button
      >
      <button
        class="bg-[#f2f9ff] border-[#338eda] text-[#338eda] hover:bg-[#338eda]"
        onclick={() => {
          window.location.href = buttonLink[1];
        }}
      >
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
        requirements</button
      >
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
<div
  class="relative bg-[#050c2e] w-full min-h-screen z-10 pb-2 px-4 md:px-12 flex flex-col items-center"
  id="how-works"
>
  <h1 class="text-[8vw] text-center">how does this work?</h1>
  <div class="w-full grid-cols-1 md:grid-cols-2 grid">
    <div class="border-blue-200 border-2 px-2 py-2 w-full">
      <h1 class="lg:text-[3vw] md:text-[5vw] text-[8vw]">1. join the slack</h1>
      <p class="lg:text-[1.2vw] md:text-[2vw] text-[4vw] font-[times_new_roman]">
        join the <a href="https://hackclub.com/slack" target="_blank" class="text-blue-200 underline">hack club slack</a
        >! you'll join a community of other teens with common interests in coding, game development, hardware, and other
        cool stuff. <br /><br />
        once you join, you can introduce yourself in the #welcome channel.
      </p>
      <br />
      <p class="lg:text-[1.2vw] md:text-[2vw] text-[4vw] font-[times_new_roman]">
        the #joystick channel is where we'll post updates about this specific program.
        <br />
        this is where you can ask any questions you have, share your progress, and get feedback on your game. it's also a
        great place to connect with other people who are making games!
      </p>
    </div>

    <div class="border-blue-200 border-2 px-2 w-full py-2">
      <h1 class="lg:text-[3vw] md:text-[5vw] text-[8vw]">2. make a game!</h1>
      <p class="lg:text-[1.2vw] md:text-[2vw] text-[3.5vw] font-[times_new_roman]">
        think of an idea and start making! it can be anything from a story game, to a platformer, or a strategy game.<br
        /><br />
        you can use any game engine or programming language, as long as your game meets the requirements listed below.<br
        /><br />
        <span class="font-bold text-red-300 text-[110%]">important!</span> log your coding time on
        <a href="https://hackatime.hackclub.com" target="_blank">hackatime</a>
        and your art/music time on
        <a href="https://lapse.hackclub.com" target="_blank">lapse</a>!
      </p>
      <h2 class="lg:text-[1.9vw] md:text-[3vw] text-[4vw] mt-[2vh]">what if i don't know how to make a game?</h2>
      <div class="lg:text-[1.2vw] md:text-[2vw] text-[4vw] font-[times_new_roman]">
        <p>there's tons of resources online to help you get started! here's a few:</p>
        <ul class="list-disc list-inside">
          <li>
            <a href="https://workshops.hackclub.com#games" target="_blank"> hack club game development workshops! </a>
            <!-- i've done some of those workshops and they're goated -->
          </li>
          <li>
            <a href="https://www.youtube.com/@Brackeys" target="_blank">brackeys youtube channel</a>
            (i'll recommend his godot tutorial)
          </li>
        </ul>
      </div>
    </div>
    <div class="border-blue-200 border-2 px-2 w-full py-2">
      <h1 class="lg:text-[3vw] md:text-[5vw] text-[8vw]">3. submit your game!</h1>
      <div class="lg:text-[1.2vw] md:text-[2vw] text-[4vw] font-[times_new_roman]">
        <div>
          <input type="checkbox" disabled checked /> have you met all the <a href="#requirements">requirements</a>?
        </div>
        <div>
          <input type="checkbox" disabled checked /> have you logged your coding time on hackatime and art/music time on
          lapse?
        </div>
        <div>
          <input type="checkbox" disabled checked /> do you have enough potential tokens to redeem the arcade machine parts
          you want?
        </div>
        <p class="mt-[2vh]">
          use <a href="# yo add this link later"> this </a> form to submit your game for review!<br /> once you submit,
          our team will review your game and add the tokens to your account. <br />if we have any feedback, we'll DM you
          on slack.
        </p>
      </div>
    </div>
    <div class="border-blue-200 border-2 px-2 w-full py-2">
      <h1 class="lg:text-[3vw] md:text-[5vw] text-[8vw]">4. get your arcade machine!</h1>
      <p class="lg:text-[1.2vw] md:text-[2vw] text-[3.5vw] font-[times_new_roman]">
        redeem your tokens for arcade machine parts at the <a href="#yo add this link later">ordering page</a>! our team
        will ship the parts to you and help you with any questions you have about assembling or programming your arcade
        machine. <br /><br />
        once you assemble your arcade machine, share a video of it on the #joystick channel on slack. we'd love to see it!
      </p>
    </div>
  </div>
  <div class="w-full items-center justify-center flex mt-[2vh] bottom-2">
    <p>
      have any questions? ask us on <a href="https://hackclub.com/slack" target="_blank" class="text-blue-200 underline"
        >slack</a
      >!
    </p>
  </div>
</div>
<div
  class="relative bg-[#050c2e] w-full min-h-screen z-10 pb-2 px-4 md:px-12 flex flex-col items-center"
  id="requirements"
>
  <h1 class="text-[12vw] text-center">requirements</h1>
  <div class="w-full items-center justify-center flex">
    <ol
      class="list-decimal list-inside items-start justify-center px-4 text-lg md:text-xl lg:text-2xl flex flex-col gap-8 md:gap-10"
    >
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
          we strongly recommend building your game to the web: it'll be accessible to more people and will speed up the
          review process.
        </span>
      </li>
      <li class="list-item text-purple-400">
        you must log your time using hackatime and lapse. <br />
        <span class="font-[times_new_roman] text-white text-lg">
          check out <a href="https://hackatime.hackclub.com" target="_blank" class="text-blue-200 underline"
            >hackatime</a
          >
          and <a href="https://lapse.hackclub.com" target="_blank" class="text-blue-200 underline">lapse</a> at those links.
          we'll use these to calculate how many tokens you've earned. log your time honestly!
        </span>
      </li>
    </ol>
  </div>
</div>
