<script lang="ts">
    import {createEventDispatcher} from "svelte";

    export let title: string;
    export let disabled = false;
    export let secondary = false;
    export let inset = false;
    export let listenForEnter = false;

    const dispatch = createEventDispatcher();

    function handleKeyDown(e: KeyboardEvent) {
        if (!listenForEnter) {
            return;
        }
        if (e.key === "Enter") {
            dispatch("click");
        }
    }
</script>

<svelte:window on:keydown={handleKeyDown}/>
<button class="button-setting" class:inset type="button" on:click={() => dispatch("click")} {disabled} class:secondary>{title}</button>

<style lang="scss">
  @import "../../../../colors.scss";

  .button-setting {
    border: none;
    background-color: $accent-color;
    color: $text-color;
    font-family: "Inter", sans-serif;
    padding: 20px;
    border-radius: 12px;
    font-size: 20px;
    transition: ease background-color .2s, ease opacity .2s;

    &.inset {
      margin: 0 30px;
    }

    &.secondary {
      background-color: rgba($background-color, 0);
    }

    &:not([disabled]):hover {
      background-color: darken(desaturate($accent-color, 0%), 0%);
      cursor: pointer;

      &.secondary {
        background-color: darken(desaturate($background-color, 0%), 0%);
      }
    }

    &[disabled] {
      opacity: .6;
    }
  }
</style>