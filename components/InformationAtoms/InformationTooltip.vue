<template>
    <div class="relative group">
      <!-- Tooltip Trigger -->
      <div
        class="bg-zinc-700 hover:bg-zinc-900 rounded w-8 aspect-square m-10 "
      >
        <InformationSvg />
        
       
      </div>
       <!-- Tooltip Content -->
       <div
          class="absolute left-1/2 transform -translate-x-1/2  mt-2 hidden group-hover:flex flex-col items-center bg-zinc-800 text-zinc-100 text-sm rounded-lg shadow-lg p-3 max-w-xs z-10 select-text"
        >
        <div
            class="absolute bottom-full -top-1 mb-1 w-3 h-3 bg-zinc-800 rotate-45 wizardPointer select-none	"
          ></div>
          
          <p>{{ truncatedTooltipText }}</p>
          <hr class="w-64 h-px mt-5 mb-3 bg-gray-200 border-0 dark:bg-gray-700">
          More Information
        </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from "vue";
  import InformationSvg from "./InformationSvg.vue";
  
  // Full text
  const tooltipText = ref(
    "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum"
  );
  
  // Max character length
  const MAX_LENGTH = 140;
  
  // Trim text w/ "..."
  const truncatedTooltipText = computed(() =>
    tooltipText.value.length > MAX_LENGTH
      ? tooltipText.value.slice(0, MAX_LENGTH) + "..."
      : tooltipText.value
  );
  </script>
  