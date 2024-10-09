<template>
  <button
    @click="$emit('click')"
    :class="{
      'border-b-2 p-4': true,
      'border-transparent': !isActive,
      'border-b-blue-600 text-blue-600': isActive,
    }"
  >
    {{ tab.label }}
  </button>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import type { Tab } from '@/types';

const props = defineProps<{
  currentTab: string;
  tab: Tab;
}>();

defineEmits<{
  click: [];
}>();

const isActive = computed(() => props.currentTab === props.tab.key);
</script>
