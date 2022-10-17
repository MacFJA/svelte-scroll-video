<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  let node;
  let main;
  let y = 0;
  let wasPlaying = false;

  export let pixelPerSec = 1000;

  /**
   * Set the dimension of the video "track"
   */
  function init() {
    const maxHeight = (node.duration || 0) * pixelPerSec;
    main.style.height = maxHeight + node.clientHeight + "px";
  }

  /**
   * Set the position of video
   */
  function play() {
    const duration = node.duration || 0;
    const time = node.offsetTop / pixelPerSec;
    const playing = time > 0 && time < duration;

    // Update video position
    node.currentTime = minMax(0, time, duration);

    // Send events
    if (playing !== wasPlaying) dispatch("playing", playing);
    if (playing) dispatch("position", time);

    wasPlaying = playing;
  }

  /**
   * Return a value that won't outbound its limits
   * @param {number} min The minimum value allowed
   * @param {number} value The input value
   * @param {number} max The maximum value allowed
   * @return {number}
   */
  function minMax(min, value, max) {
    return Math.max(min, Math.min(value, max));
  }

  $: if (y) play();
</script>

<svelte:window bind:scrollY={y} />

<main bind:this={main}>
  <video bind:this={node} on:durationchange={init} {...$$restProps}>
    <track kind="captions" />
    <slot />
  </video>
</main>

<style>
  main {
    position: relative;
    background: var(--video-background, transparent);
    padding-top: 0 !important; /* MUST be 0, otherwise the video is always playing */
  }
  video {
    margin-top: 0 !important; /* MUST be 0, otherwise the video is always playing */
    position: sticky;
    top: 0;
    bottom: 0;
    width: 100%;
    height: var(--video-height, 100vh);
  }
</style>
