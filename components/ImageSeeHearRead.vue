<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    filename: {
      type: String,
      required: true,
    },
    altValue: {
      type: String,
      required: false,
    },
  },
  computed: {
    screenReader() {
      return `Image: ${this.altValue || this.filename}`;
    },
  },
});
</script>

<template>
  <div
    class="flex flex-1 flex-row gap-8 rounded-2xl border-2 border-blue-4 bg-blue-3-light p-8 pt-6 shadow-small-drop-shadow *:flex *:flex-1 *:flex-col *:items-center *:gap-4 dark:bg-blue-3-dark"
  >
    <div title="What a sighted user sees">
      <Icon name="mdi:eye-outline" size="2rem" />
      <div
        class="flex flex-1 self-stretch *:flex-1 *:self-stretch *:rounded-2xl *:object-cover"
      >
        <slot>
          <img src="~/assets/img/axolotl-1.jpg" alt="axolotl in an aquarium" />
        </slot>
      </div>
    </div>

    <div title="What a screen reader reads out loud">
      <Icon name="material-symbols:hearing" size="2rem" />
      <div
        class="grid flex-1 place-items-center self-stretch text-pretty rounded-2xl bg-blue-5-light p-4 text-center shadow-small-drop-shadow dark:bg-blue-5-dark forced-colors:outline"
      >
        <p>{{ screenReader }}</p>
      </div>
    </div>

    <div title="What a user with bad internet connection sees">
      <Icon name="ic:twotone-wifi-off" size="2rem" />

      <div
        class="grid flex-1 place-items-center self-stretch rounded-2xl bg-blue-5-light p-4 shadow-small-drop-shadow dark:bg-blue-5-dark forced-colors:outline"
      >
        <p>
          <Icon name="material-symbols:broken-image-rounded" />
          <span class="sr-only">broken image</span>
          {{ altValue || filename }}
        </p>
      </div>
    </div>
  </div>
</template>

<style></style>
