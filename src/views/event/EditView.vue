<script setup lang="ts">
import { toRefs } from 'vue'
import { type Event } from '@/types'
import router from '@/router'
import { useMessageStore } from '@/stores/message'

const props = defineProps<{
  event: Event
  id: String
}>()

const { event } = toRefs(props)
const store = useMessageStore()

const saveChanges = () => {
  store.updateMessage('Your changes have been saved for ' + props.event.title)
  setTimeout(() => {
    store.resetMessage()
  }, 3000)
  router.push({ name: 'event-detail-view', params: { id: props.event.id }})
}
</script>

<template>
  <p>Edit event here</p>
  <!-- สามารถเพิ่มฟอร์มแก้ไข event ได้ที่นี่ -->
  <button @click="saveChanges">Save</button>
</template>
