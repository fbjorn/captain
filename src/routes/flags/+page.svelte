<script lang="ts">
  import { FLAGS } from "./config"
</script>

<div class="table">
  {#each Object.values(FLAGS) as flag}
    <div class="flag">
      <div class="letter">{flag.letter}</div>
      <img src={flag.src} alt={flag.word} />
      <p>{flag.word}</p>
      <p>{flag.meaning}</p>
    </div>
    <div class="divider"></div>
  {/each}
</div>

<style lang="scss">
  .header {
    padding: 1rem 0 2rem;
  }

  .table {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    max-width: 40rem;
    margin: 0 auto;

    .divider {
      height: 1px;
      width: 100%;
      border-bottom: 1px solid lightgray;
    }
  }

  .flag {
    display: grid;
    grid-template-columns: 2rem 3rem 7rem auto;
    align-items: center;

    img {
      width: 2rem;
    }

    .letter {
      font-weight: 600;
    }
  }
</style>
