<script lang="ts">
  import { FLAGS } from "../config"
  import { Button, TextInput } from "carbon-components-svelte"
  import { onMount } from "svelte"

  const flagsArray = Object.values(FLAGS)

  let flag = undefined
  let text = ""

  let answered = false
  let gaveUp = false
  let valid = false

  $: finished = valid || gaveUp

  function pickFlag() {
    return flagsArray[Math.floor(Math.random() * 26)]
  }

  onMount(() => {
    flag = pickFlag()
  })

  function check() {
    valid = flag.word.toLowerCase() === text.trim().toLowerCase()
    answered = true
    if (valid) {
      text = ""
    }
  }

  function giveUp() {
    gaveUp = true
    text = ""
  }

  function next() {
    text = ""
    gaveUp = false
    valid = false
    answered = false
    for (let i = 0; i < 10; i++) {
      const newFlag = pickFlag()
      if (newFlag.letter !== flag.letter) {
        flag = newFlag
        break
      }
    }
  }
</script>

<div class="flag-quiz">
  {#if flag}
    <img src={flag.src} alt={flag.word} />
  {/if}
  <form>
    <TextInput bind:value={text} placeholder="Enter flag name" />
    <div class="buttons">
      <Button type="submit" on:click={check} disabled={finished}>Check</Button>
      <Button on:click={giveUp} disabled={finished}>Give up</Button>
      {#if finished}
        <Button on:click={next}>Next</Button>
      {/if}
    </div>
  </form>
  {#if answered && !gaveUp}
    <div class:right={valid} class:wrong={!valid}>
      {valid ? "Correct" : "Wrong"}
    </div>
  {/if}
  {#if (answered && valid) || gaveUp}
    <div class="answer">
      <div class="word">{flag.word}</div>
      <p class="meaning">{flag.meaning}</p>
    </div>
  {/if}
</div>

<style lang="scss">
  .flag-quiz {
    max-width: 30rem;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
  }

  img {
    width: 10rem;
    border: 2px solid black;
    border-radius: 2px;
    margin-bottom: 1rem;
    align-self: center;
  }
  .buttons {
    display: flex;
    gap: 1rem;
    margin: 1rem 0;
    flex-wrap: wrap;
  }

  .answer {
    .word {
      font-size: 1.25rem;
      font-weight: 500;
      padding: 0.5rem 0;
    }
    .meaning {
      font-style: italic;
    }
  }
</style>
