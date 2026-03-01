<script setup lang="ts">
const emit = defineEmits<{
  (e: "submit", value: string): void;
}>();

const accountName = defineModel<string>({
  default: "",
});

function handleSubmit() {
  emit("submit", accountName.value.toLowerCase());
}

const inputRef = useTemplateRef("inputRef");
function clear() {
  accountName.value = "";
  inputRef.value?.focus();
}
</script>

<template>
  <form @submit.prevent="handleSubmit" class="flex mb-8">
    <div
      class="w-full flex rounded-lg overflow-hidden bg-gh-card focus-within:ring-1 focus-within:ring-gh-blue/50"
    >
      <div class="flex-1 relative flex items-center">
        <label class="sr-only" for="userName">Enter GitHub username</label>
        <input
          v-model="accountName"
          ref="inputRef"
          id="userName"
          placeholder="Enter GitHub username..."
          class="w-full py-2.5 px-4 bg-transparent text-gh-text text-base outline-none placeholder:text-gh-muted/60 focus:ring-0 transition-colors duration-200"
        />
        <button
          v-if="accountName"
          type="button"
          @click="clear"
          class="absolute rounded-full hover:bg-gh-muted/25 transition-all duration-200 ease-out size-5 items-center justify-center text-gh-text/70 hover:text-gh-text flex top-1/2 right-4 -translate-y-1/2"
        >
          <span class="i-carbon:close text-sm" />
        </button>
      </div>

      <div class="w-px bg-gh-border/40"></div>

      <button
        type="submit"
        class="px-6 bg-gh-green text-white hover:bg-gh-green-hover flex items-center gap-2 transition-all duration-200 ease-out font-medium text-sm"
      >
        <span class="i-carbon-search text-base" aria-hidden="true" />
        Analyze
      </button>
    </div>
  </form>
</template>
