<script setup lang="ts">
import { usePreferredDark } from "@vueuse/core";

const darkMode = usePreferredDark();
const colorMode = useColorMode();
const colorScheme = computed(() => {
  return {
    system: darkMode ? "dark light" : "light dark",
    light: "only light",
    dark: "only dark",
  }[colorMode.preference];
});

useHead({
  title: "AgentScan - GitHub AI Agent Detector",
  meta: [
    { property: "og:title", content: "AgentScan - GitHub AI Agent Detector" },
    {
      property: "og:description",
      content: "An open experiment in detecting automation patterns on GitHub",
    },
    { property: "og:type", content: "website" },
    { name: "color-scheme", content: colorScheme },
  ],
  link: [
    {
      rel: "icon",
      href: "/favicon.ico",
      type: "image/x-icon",
      media: "(prefers-color-scheme: dark)",
    },
    {
      rel: "icon",
      href: "/favicon-dark.ico",
      type: "image/x-icon",
      media: "(prefers-color-scheme: light)",
    },
  ],
});

const route = useRoute();
const isHomePage = computed<boolean>(() => route.name === "index");
</script>

<template>
  <NuxtLoadingIndicator />

  <div class="flex flex-col">
    <div class="min-h-svh flex flex-col">
      <header class="h-12 flex justify-end items-center px-6 py-4">
        <nav>
          <ul class="flex items-center gap-6">
            <li>
              <NuxtLink
                to="/health"
                class="text-gh-muted hover:text-gh-text transition-colors"
              >
                Ecosystem health
              </NuxtLink>
            </li>
            <li class="w-px h-4 bg-gh-border/80"></li>
            <li>
              <NuxtLink
                external
                target="_blank"
                title="RSS feed"
                to="/feed.xml"
                aria-label="RSS feed"
                class="flex items-center justify-center text-gh-muted hover:text-gh-text transition-colors"
              >
                <span class="i-carbon:rss text-sm" aria-hidden="true"></span>
              </NuxtLink>
            </li>
            <li>
              <NuxtLink
                external
                target="_blank"
                title="GitHub repository"
                to="https://github.com/MatteoGabriele/agentscan"
                aria-label="GitHub repository"
                class="flex items-center justify-center text-gh-muted hover:text-gh-text transition-colors"
              >
                <span
                  class="i-carbon:logo-github text-sm"
                  aria-hidden="true"
                ></span>
              </NuxtLink>
            </li>
          </ul>
        </nav>
      </header>

      <div class="flex flex-1 items-center justify-center">
        <main class="max-w-screen-md mx-auto px-4 py-20 @container w-full">
          <MainLogo :heading-level="isHomePage ? 'h1' : 'h2'" />

          <slot />
        </main>
      </div>
    </div>

    <MainFooter />
  </div>
</template>
