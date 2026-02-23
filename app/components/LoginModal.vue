<script setup lang="ts">
const route = useRoute();

const handle = ref<string>("");
const isPending = ref<boolean>(false);
async function handleSubmit() {
  isPending.value = true;
  const { url } = await $fetch("/api/auth/login", {
    method: "POST",
    body: {
      redirectTo: route.fullPath,
    },
  });
  window.location.href = url;
}

onMounted(() => {
  document.body.classList.add("overflow-hidden");
});

onUnmounted(() => {
  document.body.classList.remove("overflow-hidden");
});

const emits = defineEmits(["close"]);
function closeModal() {
  emits("close");
}
</script>

<template>
  <div class="fixed inset-0 bg-gh-bg/90 z-50 flex items-center justify-center">
    <div
      class="bg-gh-card border-1 border-solid border-gh-border rounded-2 shadow-xl w-full max-w-sm p-6 relative"
    >
      <header class="flex items-center justify-between">
        <span
          class="i-carbon-scan text-xl text-gh-green block"
          aria-hidden="true"
        />

        <button
          @click="closeModal"
          class="size-8 flex items-center justify-center text-gh-muted hover:bg-gh-muted/20 rounded-full transition-colors"
          aria-label="Close login modal"
        >
          <span class="i-carbon-close text-xl" />
        </button>
      </header>

      <div class="my-6 text-center">
        <h2 class="text-2xl font-semibold text-gh-text mb-1">
          Sign in to AgentScan
        </h2>
        <p class="text-gh-muted text-sm">
          Connect with your
          <NuxtLink to="https://bsky.app" class="underline hover:text-gh-text"
            >Bluesky</NuxtLink
          >
          account
        </p>
      </div>
      <form @submit.prevent="handleSubmit" class="flex flex-col gap-4">
        <button
          type="submit"
          class="py-2 px-6 bg-gh-green rounded-md text-white hover:bg-gh-green-hover flex justify-center items-center gap-2 transition-colors"
        >
          <span
            v-if="isPending"
            class="i-carbon-circle-dash animate-spin text-lg"
          />
          <template v-else>
            <span class="i-carbon:logo-bluesky text-lg" aria-hidden="true" />
            Connect to Bluesky
          </template>
        </button>
      </form>
    </div>
  </div>
</template>
