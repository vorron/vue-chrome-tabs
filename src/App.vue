<script setup lang="ts">
import { ref, type Ref } from 'vue'
import type { Tab } from '@/components/VueTabsChrome.vue'
import VueTabsChrome from './components/VueTabsChrome.vue'
import TheWelcome from './components/TheWelcome.vue'

const tabs: Ref<Tab[]> = ref([
  { label: 'google', key: 'google', favicon: 'https://img.icons8.com/color/google' },
  { label: 'facebook', key: 'facebook', favicon: 'https://img.icons8.com/color/facebook' },
  { label: 'linkedin', key: 'linkedin', favicon: 'https://img.icons8.com/color/linkedin' },
  { label: 'twitter', key: 'twitter', favicon: 'https://img.icons8.com/color/twitter' },
  { label: 'instagram', key: 'instagram', favicon: 'https://img.icons8.com/color/instagram' }
])
const tab = ref(tabs.value[0].key ?? '')

const event = ref('')

const onActivate = (value: string) => {
  event.value = 'click tab: ' + value
}

const onClose = (value: any) => {
  event.value = 'close tab: ' + value
  const result = confirm('You really want to close this wonderful tab?')
  if (result) {
    tabs.value.splice(
      tabs.value.findIndex((e) => e.key === value),
      1
    )
  }
}
</script>

<template>
  <vue-tabs-chrome @activate="onActivate" :tabs="tabs" v-model="tab" @close="onClose" />
  <p class="info"><strong>active tab: </strong>{{ tab }}</p>
  <p class="info"><strong>event: </strong>{{ event }}</p>
</template>

<style scoped>
.info {
  font-size: 26px;
  margin-top: 10px;
  margin-left: 10px;
}
strong {
  font-weight: 900;
}
</style>
