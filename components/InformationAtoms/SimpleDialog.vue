<template>
    <transition name="fade">
      <div
        v-if="modelValue"
        class="fixed inset-0 flex items-center justify-center bg-black/50 z-50"
        @click.self="closeDialog"
      >
        <div class="bg-white p-5 rounded-lg shadow-lg max-w-lg w-full">
          <button
            class="ml-auto block mb-4 text-gray-600 hover:text-gray-900"
            @click="closeDialog"
          >
            ✕
          </button>
          <slot></slot>
        </div>
      </div>
    </transition>
  </template>
  
  <script setup>
  const props = defineProps({
    modelValue: {
      type: Boolean,
      required: true,
    },
  });
  
  const emit = defineEmits(["update:modelValue"]);
  
  const closeDialog = () => {
    emit("update:modelValue", false);
  };
  </script>
  
  <style scoped>
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.3s ease;
  }
  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
  }
  </style>
  