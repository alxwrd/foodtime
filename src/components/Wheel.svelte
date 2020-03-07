<script>
  import Winwheel from "./Winwheel.js";
  import { createEventDispatcher } from "svelte";
  import { onMount } from "svelte";

  const dispatch = createEventDispatcher();

  let wheel;

  export let width = "500";
  export let height = "500";

  onMount(() => {
    fetch("https://api.jsonbin.io/b/5e638151763fa966d411d5b2/latest")
      .then(response => {
        return response.json();
      })
      .then(json => {
        wheel = new Winwheel({
          canvasId: "wheel",
          pointerAngle: 90,
          numSegments: 15,
          innerRadius: 60, // Set inner radius to make wheel hollow.
          textFontSize: 16, // Set font size accordingly.
          textMargin: 0, // Take out default margin.
          // Define segments including colour and text.
          segments: json.segments,
          // Define spin to stop animation.
          animation: {
            type: "spinToStop",
            duration: 20,
            spins: 13,
            callbackFinished: alertPrize,
            easing: "back.out(0.2)"
          }
        });
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

<div class="text-center p-4 mx-auto">
  <canvas id="wheel" {width} {height} class="w-full">
    Canvas not supported, use another browser.
  </canvas>

  <div
    class="block relative text-2xl"
    style="top: -50%; right: -50%; transform:translateY(70%);">
    <span>👈</span>
  </div>

  <button
    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 border
    border-blue-700 rounded m-4"
    on:click={spin}>
    SPIN
  </button>
</div>
