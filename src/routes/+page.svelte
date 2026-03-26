<script lang="ts">
  import { onMount } from "svelte";

  var scrollY = $state(window.scrollY);
  window.onscroll = () => {
    scrollY = window.scrollY;
  };

  let canvas: HTMLCanvasElement;

  // load image as promsie
  const loadImage = (src: string): Promise<HTMLImageElement> => {
    return new Promise((resolve, reject) => {
      const img = new Image();
      img.src = src;
      img.onload = () => resolve(img);
      img.onerror = reject;
    });
  };

  const pages = ["#bg", "#how-works", "#requirements"];
  let currentPage = $state(window.location.hash || "#bg");
  document.onkeydown = (e) => {
    if (e.key === "s") {
      const currentIndex = pages.indexOf(currentPage);
      const nextPage = pages[currentIndex + 1] || pages[0];
      window.location.hash = nextPage;
      currentPage = nextPage;
    } else if (e.key === "w") {
      const currentIndex = pages.indexOf(currentPage);
      const prevPage = pages[currentIndex - 1] || pages[pages.length - 1];
      window.location.hash = prevPage;
      currentPage = prevPage;
    }
  };
  window.onscroll = () => {
    const scrollPosition = window.scrollY;
    const pageHeight = window.innerHeight;
    const pageIndex = Math.round(scrollPosition / pageHeight);
    currentPage = pages[pageIndex] || "#bg";
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

{#if !mobileCheck()}
  <div class="absolute right-2 top-1 bg-white text-black z-30 flex flex-col gap-2 px-2 py-2 text-sm md:text-base">
    <div class="flex flex-row items-center gap-2">
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
    <div class="flex flex-row items-center gap-2">
      <input
        type="checkbox"
        onchange={(e) => {
          if ((e.target as HTMLInputElement).checked) {
            document.documentElement.setAttribute("data-theme", "dark");
          } else {
            document.documentElement.removeAttribute("data-theme");
          }
        }}
      />
      <p class="font-[Times_New_Roman,serif]">enable dark mode</p>
    </div>
  </div>
{/if}
<main class="w-full h-full dark:bg-[#050c2e] bg-[#99d9ea]" id="bg">
  <img
    class="absolute md:bottom-[10vh] bottom-[20vh] md:left-[4vw] left-[1vw] rotate-15 md:w-[35vw] w-[60vw]"
    alt="arcade machine"
    src="/images/arcademachine.png"
  />
  <img class="absolute bottom-[14vh] right-[4vw] -rotate-15 w-[35vw]" alt="controller" src="/images/controller-1.png" />
  <div class="absolute flex flex-col gap-2 z-10 w-full">
    <h1
      class="lg:text-[14vw] md:text-[18vw] text-[17vw] text-center lg:mt-[3%] md:mt-[15%] mt-[30%] gap-0 h-fit"
      id="title"
    >
      <span class="animate-[flicker_4s_infinite]">&#91;</span>
      <span class="animate-[stutterglitch_4s_infinite]">j</span>
      <span class="animate-[glitchfast_4s_infinite]">o</span>
      <span class="animate-[flicker_5s_infinite]">y</span>
      <span class="animate-[glitchfast_3s_infinite]">s</span>
      <span class="animate-[stutterglitch_4s_infinite]">t</span>
      <span class="animate-[glitchfast_4s_infinite]">i</span>
      <span class="animate-[glitchfast_4s_infinite]">c</span>
      <span class="animate-[glitchfast_5s_infinite]">k</span>
      <span class="animate-[stutterglitch_4s_infinite]">&#93;</span>
    </h1>
    <div class="text-center w-full flex justify-center gap-4">
      <div class="bg-[#99d9ea] dark:bg-[#050c2e] flex flex-col items-center">
        <p class="text-[clamp(1.5rem,3vw,2rem)] dark:bg-[#050c2e] bg-[#99d9ea] opacity-90 w-fit">make a game, get an</p>
        <b class="text-[300%] bg-[#99d9ea] dark:bg-[#050c2e]">arcade machine!</b>
        <p class="text-[clamp(1rem,2.2vw,1.2rem)] dark:bg-[#050c2e] bg-[#99d9ea] w-fit">
          june 22nd, 2026 - july 17th, 2026
        </p>
      </div>
    </div>
  </div>
  <div class="z-30 absolute lg:bottom-2 md:bottom-4 bottom-8 right-2 bg-white dark:bg-black px-2 py-2">
    <p>
      made with ❤️ by <a href="https://hackclub.com" target="_blank">hack club</a>
    </p>
    <div class="flex flex-row gap-2">
      <a href="https://github.com/tiredkangaroo/joystick" target="_blank">open source!</a>
      |
      <a href="https://hackclub.com/slack" target="_blank">join the slack!</a>
    </div>
  </div>
</main>
<div
  class="relative dark:bg-[#050c2e] bg-[#99d9ea] w-full min-h-screen z-10 pb-2 px-4 md:px-12 flex flex-col items-center"
  id="how-works"
>
  <h1 class="text-[8vw] text-center">how does this work?</h1>
  <div class="w-full grid-cols-1 md:grid-cols-2 grid gap-2">
    <div class="dark:border-blue-200 border-blue-900 border-2 px-2 py-2 w-full">
      <h1 class="lg:text-[3vw] md:text-[5vw] text-[8vw]">1. join the slack</h1>
      <p class="lg:text-[1.2vw] md:text-[2vw] text-[4vw] font-[times_new_roman]">
        join the <a href="https://hackclub.com/slack" target="_blank" class="text-blue-200 underline">hack club slack</a
        >! you'll join a community of other teens with common interests in coding, game development, hardware, and other
        cool stuff. <br /><br />
        once you join, you can introduce yourself in the #welcome channel.
      </p>
      <br />
      <h2 class="lg:text-[2vw] md:text-[4vw] text-[6vw]">the #joystick channel</h2>
      <p class="lg:text-[1.2vw] md:text-[2vw] text-[4vw] font-[times_new_roman]">
        the #joystick channel is where we'll post updates about this program.
        <br /><br />
        this is where you can ask any questions you have, share your progress, and get feedback on your game. it's also a
        great place to connect with other people who are making games!
      </p>
      <br />
      <p class="font-[times_new_roman] lg:text-[1.2vw] md:text-[2vw] text-[4vw]">
        <span class="font-bold dark:text-red-300 text-red-800 text-[110%]">important!</span>
        you're going to need to be on the hack club slack to participate in joystick!
      </p>
    </div>

    <div class="dark:border-blue-200 border-blue-900 border-2 px-2 w-full py-2">
      <h1 class="lg:text-[3vw] md:text-[5vw] text-[8vw]">2. make a game!</h1>
      <p class="lg:text-[1.2vw] md:text-[2vw] text-[3.5vw] font-[times_new_roman]">
        think of an idea and start making! it can be anything from a story game, to a platformer, to a strategy game. it
        doesn't have to be conventional: make <i>whatever</i> you want!<br /><br />
        you can use any game engine or programming language, as long as your game meets the requirements listed below.<br
        /><br />
        <span class="font-bold dark:text-red-300 text-red-800 text-[110%]">important!</span> log your coding time on
        <a href="https://hackatime.hackclub.com" target="_blank">hackatime</a>
        and your art/music time on
        <a href="https://lapse.hackclub.com" target="_blank">lapse</a>! this will be used to calculate how many tokens
        you've earned, which you'll use to redeem your arcade machine parts.
      </p>
      <h2 class="lg:text-[1.9vw] md:text-[3vw] text-[4vw] mt-[2vh]">what if i don't know how to make a game?</h2>
      <div class="lg:text-[1.2vw] md:text-[2vw] text-[4vw] font-[times_new_roman]">
        <p>there's tons of resources online to help you get started! here's two of my favorites:</p>
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
        <br />
        <p>
          project based learning is great! make your project, and when you don't know how to do something specific, find
          a tutorial or ask for help!
        </p>
      </div>
    </div>
    <div class="dark:border-blue-200 border-blue-900 border-2 px-2 w-full py-2">
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
          use <a
            onclick={() => {
              alert("the submission form isn't ready yet! this event is not currently running :)");
            }}
          >
            this
          </a>
          form to submit your game for review!<br /> once you submit, our team will review your game and add the tokens
          to your account. <br />if we have any feedback, we'll DM you on slack.
        </p>
      </div>
    </div>
    <div class="dark:border-blue-200 border-blue-900 border-2 px-2 w-full py-2">
      <h1 class="lg:text-[3vw] md:text-[5vw] text-[8vw]">4. get your arcade machine!</h1>
      <p class="lg:text-[1.2vw] md:text-[2vw] text-[3.5vw] font-[times_new_roman]">
        redeem your tokens for arcade machine parts at the <a
          onclick={() => {
            alert("the ordering page is getting it's final garnish right now! this event is not currently running :)");
          }}>ordering page</a
        >! our team will ship the parts to you and help you with any questions you have about assembling your arcade
        machine.
        <br /><br />
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
  class="relative dark:bg-[#050c2e] bg-[#99d9ea] w-full min-h-screen z-10 pb-2 px-4 md:px-12 flex flex-col items-center"
  id="requirements"
>
  <div class="flex flex-row items-center-safe w-full justify-center">
    <h1 class="text-[12vw] text-center">requirements</h1>
  </div>
  <div class="w-full items-center justify-center flex">
    <ol
      class="list-decimal list-inside items-start justify-center px-4 text-lg md:text-xl lg:text-2xl flex flex-col gap-8 md:gap-10"
    >
      <li class="list-item dark:text-red-300 text-red-800">
        you must be <b class="font-[times_new_roman]">13-18 years old</b>. hack club is a teen community!
      </li>
      <li class="list-item dark:text-orange-300 text-orange-800">
        your game must be original. avoid copying existing games. <br />
        <span class="dark:text-white text-black text-lg font-[times_new_roman]"
          >we want to see your creativity shine! if your game is similar to an existing game, make sure to add your own
          unique twist.</span
        >
      </li>
      <li class="list-item dark:text-yellow-300 text-yellow-800">
        your game should be fun and engaging!<br />
        <span class="dark:text-white text-black text-lg font-[times_new_roman]"
          >aim for five minutes of engaging gameplay.</span
        >
      </li>
      <li class="list-item dark:text-green-300 text-green-800">
        absolutely NO ai generated art, music, README, or docs. <br />
        <span class="dark:text-white text-black text-lg font-[times_new_roman]"
          >additionally, minimize the use of ai in code. we want to see your creativity, even if it's not perfect!</span
        >
      </li>
      <li class="list-item dark:text-blue-300 text-blue-800">
        your game must be open source & playable on a computer or mobile device.<br />
        <span class="dark:text-white text-black text-lg font-[times_new_roman]">
          we strongly recommend building your game to the web: it'll be accessible to more people and will speed up the
          review process.
        </span>
      </li>
      <li class="list-item dark:text-purple-300 text-purple-800">
        you must log your time using hackatime and lapse. <br />
        <span class="font-[times_new_roman] dark:text-white text-black text-lg">
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
