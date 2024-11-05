<script lang="ts">
  import { ContentSwitcher, Switch } from "carbon-components-svelte"
  import { Tabs, Tab, TabContent } from "carbon-components-svelte"

  import GuessByFlag from "./GuessByFlag.svelte"
  import GuessByMeaning from "./GuessByMeaning.svelte"

  let index = 0
</script>

<div class="wrapper">
  <Tabs autoWidth>
    <Tab label="Guess word by flag picture" />
    <Tab label="Guess word by flag meaning" />
    <svelte:fragment slot="content">
      <TabContent>
        <GuessByFlag />
      </TabContent>
      <TabContent>
        <GuessByMeaning />
      </TabContent>
    </svelte:fragment>
  </Tabs>
</div>

<style lang="scss">
  .wrapper {
    display: flex;
    flex-direction: column;
    gap: 4rem;
    max-width: 40rem;
    margin: 0 auto;

    :global(ul.bx--tabs__nav) {
      //width: 100%;
    }
  }
</style>
