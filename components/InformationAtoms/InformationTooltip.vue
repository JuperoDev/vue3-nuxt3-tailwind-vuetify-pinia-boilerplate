<template>
    <div class="relative" ref="tooltipContainer">
      <!-- Tooltip Trigger -->
      <div>
        <InformationSvg
          @click="toggleTooltip"
          :class="[ 
            'bg-zinc-700 rounded w-8 aspect-square informationSVG',
            isTooltipVisible ? 'bg-zinc-900' : 'hover:bg-zinc-900'
          ]"
        />
      </div>
  
      <!-- Tooltip Content -->
      <transition name="fade">
        <div
          v-if="isTooltipVisible"
          class="absolute left-1/2 transform -translate-x-1/2 mt-2 flex flex-col items-center bg-zinc-800 text-zinc-100 text-sm rounded-lg shadow-lg p-3 max-w-xs z-10 select-none"
        >
          <div
            class="absolute bottom-full -top-1 mb-1 w-3 h-3 bg-zinc-800 rotate-45 wizardPointer select-none"
          ></div>
  
          <p>{{ truncatedTooltipText }}</p>
          <hr class="w-64 h-px mt-5 mb-3 bg-gray-200 border-0 dark:bg-gray-700 select-none">
          <i
            class="hover:underline underline-offset-4 cursor-pointer"
            @click="showDialog"
          >
            More Information
          </i>
        </div>
      </transition>
  
      <!-- Dialog -->
      <SimpleDialog v-model="isDialogVisible">
        <p>This is additional information shown in the dialog!</p>
      </SimpleDialog>
    </div>
  </template>
  
  <script setup>
  import { ref, computed, onMounted, onUnmounted } from "vue";
  import InformationSvg from "./InformationSvg.vue";
  import SimpleDialog from "./SimpleDialog.vue";
  

  const isTooltipVisible = ref(false);
  const isDialogVisible = ref(false);
  

  const tooltipContainer = ref(null);
  

  const toggleTooltip = () => {
    isTooltipVisible.value = !isTooltipVisible.value;
  };
  
 
  const showDialog = () => {
    isTooltipVisible.value = false;
    isDialogVisible.value = true;
  };
  

  const handleClickOutside = (event) => {
    if (
      tooltipContainer.value &&
      !tooltipContainer.value.contains(event.target)
    ) {
      isTooltipVisible.value = false;
    }
  };
  

  onMounted(() => {
    document.addEventListener("click", handleClickOutside);
  });
  
  onUnmounted(() => {
    document.removeEventListener("click", handleClickOutside);
  });
  
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
  
  <style scoped>
  .informationSVG {
    margin: 0 auto;
  }
  
  /* Transition */
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.3s ease, transform 0.3s ease;
  }
  
  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
    transform: translateY(-10px);
  }
  </style>
  