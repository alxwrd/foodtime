<script>
  import Winwheel from "./Winwheel.js";
  import { createEventDispatcher } from "svelte";
  import { onMount } from "svelte";

  const dispatch = createEventDispatcher();

  let wheel;

  export let width = "500";
  export let height = "500";

  onMount(() => {
    wheel = new Winwheel({
      canvasId: "wheel",
      pointerAngle: 90,
      numSegments: 15,
      innerRadius: 60, // Set inner radius to make wheel hollow.
      textFontSize: 16, // Set font size accordingly.
      textMargin: 0, // Take out default margin.
      // Define segments including colour and text.
      segments: [
        { fillStyle: "#eae56f", text: "Spoons" },
        { fillStyle: "#89f26e", text: "Chip shop" },
        { fillStyle: "#7de6ef", text: "McDonalds" },
        { fillStyle: "#e7706f", text: "Hooters" },
        { fillStyle: "#eae56f", text: "Burger King" },
        { fillStyle: "#89f26e", text: "Greggs" },
        { fillStyle: "#7de6ef", text: "KFC" },
        { fillStyle: "#e7706f", text: "Barburrito" },
        { fillStyle: "#eae56f", text: "Taco Bell" },
        { fillStyle: "#89f26e", text: "MOD Pizza" },
        { fillStyle: "#7de6ef", text: "Five Guys" },
        { fillStyle: "#e7706f", text: "Subway" },
        { fillStyle: "#eae56f", text: "Chopstix" },
        { fillStyle: "#89f26e", text: "Via Fossa (sunny day)" },
        { fillStyle: "#7de6ef", text: "Canalhouse" }
      ],
      // Define spin to stop animation.
      animation: {
        type: "spinToStop",
        duration: 2,
        spins: 12,
        callbackFinished: alertPrize
      }
    });
  });

  // Called when the animation as finished.
  function alertPrize(indicatedSegment) {
    // Do basic alert of the segment text.
    dispatch("message", {
      text: indicatedSegment.text
    });
    wheel.rotationAngle = 0;
  }

  function spin() {
    wheel.startAnimation();
  }
</script>

<div class="text-center p-4">
  <canvas id="wheel" {width} {height} class="w-full">
    Canvas not supported, use another browser.
  </canvas>

  <div class="absolute text-2xl" style="left: {width}px; top: {(height / 2)-5}px;">
    <span>👈</span>
  </div>

  <button
    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 border
    border-blue-700 rounded m-4"
    on:click={spin}>
    SPIN
  </button>
</div>