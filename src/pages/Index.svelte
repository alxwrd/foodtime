<script>
  import Wheel from "../components/Wheel.svelte";

  import { confetti } from "dom-confetti";

  let result = "";

  function handleMessage(event) {
    result = event.detail.text;
    confetti(document.getElementById("result"));
  }
</script>

<main class="h-100">

  <div class="w-full mx-auto px-auto flex flex-wrap">
    <Wheel on:message={handleMessage} />
    <div class="m-auto text-6xl">
      <p>{result}</p>
      <div id="result" class="mx-auto w-1" />
    </div>
  </div>

</main>
