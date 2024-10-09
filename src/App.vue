<template>
  <main class="mx-auto max-w-2xl px-4">
    <nav class="mb-4 border-b border-gray-200 text-center font-medium text-gray-500">
      <ul class="-mb-px flex flex-wrap">
        <li v-for="tab in tabs" :key="tab.key">
          <TabLink :tab="tab" :current-tab="currentTab" @click="currentTab = tab.key"></TabLink>
        </li>
      </ul>
    </nav>
    <FadeTransition>
      <KeepAlive> <component :is="currentTabComponent"></component></KeepAlive>
    </FadeTransition>
    <NotificationList />
  </main>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import type { TabKey, Tab } from '@/types';

import TabLink from '@/components/TabLink.vue';
import FadeTransition from '@/components/FadeTransition.vue';
import GeneralSettings from '@/components/GeneralSettings.vue';
import NotificationsSettings from '@/components/NotificationsSettings.vue';
import PrivacySettings from '@/components/PrivacySettings.vue';
import NotificationList from '@/components/NotificationList.vue';

const tabs: Tab[] = [
  { key: 'General', label: 'General', component: GeneralSettings },
  { key: 'Notifications', label: 'Notifications', component: NotificationsSettings },
  { key: 'Privacy', label: 'Privacy', component: PrivacySettings },
];

const currentTab = ref<TabKey>('General');
const currentTabComponent = computed(
  () => tabs.find((tab) => tab.key === currentTab.value)?.component
);
</script>
