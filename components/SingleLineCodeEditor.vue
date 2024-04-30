<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      showHint: false,
      currentCode: this.defaultCode
    };
  },
  watch: {
    isCorrect(newValue) {
      if (newValue) {
        this.$emit('solved');
      }
    }
  },
  computed: {
    isCorrect(): boolean {
      return this.check(this.currentCode);
    },
  },
  methods: {
    toggleHint() {
      this.showHint = !this.showHint;
    },
    reset() {
      this.currentCode = this.defaultCode;
      this.showHint = false;
    },
  },
  props: {
    before: {
      type: String,
      required: true,
    },
    defaultCode: {
      type: String,
      required: true,
    },
    after: {
      type: String,
      required: true,
    },
    hint: {
      type: String,
      required: true,
    },
    check: {
      type: Function,
      required: true
    },
  },
  emits: ['solved'],
});
</script>
<template>
  <div
    class="flex flex-none gap-2 rounded-2xl bg-blue-3-light p-3 dark:bg-blue-5-dark"
  >
    <div
      class="flex-1 rounded-2xl bg-blue-5-light p-2 font-mono dark:bg-blue-4"
    >
      <div class="whitespace-pre-wrap">{{ before }}</div>
      <div
        v-if="showHint"
        class="whitespace-pre-wrap bg-hint-highlight-light dark:bg-hint-highlight-dark"
      >
        {{ hint }}
      </div>
      <input
        type="text"
        v-model="currentCode"
        autofocus
        autocapitalize="none"
        spellcheck="false"
        class="w-full resize-none outline-none transition-colors duration-200"
        :class="{
          'bg-input-correct-highlight': isCorrect,
          'bg-hint-highlight-light dark:bg-hint-highlight-dark': !isCorrect,
        }"
      />
      <div class="whitespace-pre-wrap">{{ after }}</div>
    </div>
    <div class="flex flex-col justify-center gap-3">
      <button
        @click="toggleHint"
        class="size-12 rounded-lg bg-axolotl-light shadow-content-box-drop-shadow hover:bg-axolotl-dark dark:bg-axolotl-dark hover:dark:bg-axolotl-light"
      >
        <Icon name="lucide:lightbulb" class="size-8" />
      </button>
      <button
        @click="reset"
        class="size-12 rounded-lg bg-blue-5-light shadow-content-box-drop-shadow hover:bg-blue-5-dark dark:bg-blue-4 hover:dark:bg-blue-2-dark"
      >
        <Icon name="lucide:rotate-ccw" class="size-7" />
      </button>
    </div>
  </div>
</template>
<style></style>