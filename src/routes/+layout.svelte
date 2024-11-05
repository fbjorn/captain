<script lang="ts">
  import "carbon-components/css/carbon-components.min.css"
  import {
    Header,
    HeaderNav,
    HeaderNavItem,
    SkipToContent,
    Content
  } from "carbon-components-svelte"

  let isSideNavOpen = false
</script>

<Header platformName="Captain little helper" bind:isSideNavOpen>
  <svelte:fragment slot="skip-to-content">
    <SkipToContent />
  </svelte:fragment>
  <HeaderNav>
    <HeaderNavItem href="/" text="Home" />
    <HeaderNavItem href="/flags" text="Flags" />
    <HeaderNavItem href="/flags/quiz" text="Flags quiz" />
  </HeaderNav>
</Header>

<Content>
  <slot />
</Content>

<style>
</style>
