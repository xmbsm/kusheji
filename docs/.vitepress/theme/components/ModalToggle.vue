<template>
  <div ref="toggleRef" class="modal-toggle-wrapper">
    <span class="modal-toggle-divider"></span>
    <div class="modal-toggle" @click="toggle" :title="showModal ? '当前：弹窗打开文章，点击切换为直接跳转' : '当前：直接跳转文章，点击切换为弹窗打开'">
      <svg v-if="showModal" class="toggle-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <rect x="2" y="3" width="20" height="14" rx="2" ry="2"></rect>
        <line x1="8" y1="21" x2="16" y2="21"></line>
        <line x1="12" y1="17" x2="12" y2="21"></line>
      </svg>
      <svg v-else class="toggle-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"></path>
        <polyline points="15 3 21 3 21 9"></polyline>
        <line x1="10" y1="14" x2="21" y2="3"></line>
      </svg>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed, onMounted } from 'vue'
import { useSettingsStore } from '../../store/settings'

const settings = useSettingsStore()
const toggleRef = ref<HTMLElement | null>(null)

const showModal = computed(() => settings.showModal)

const toggle = () => {
  settings.toggleModal()
}

onMounted(() => {
  settings.init()
  const socialLinks = document.querySelector('.VPSocialLinks')
  if (socialLinks && toggleRef.value) {
    socialLinks.parentNode?.insertBefore(toggleRef.value, socialLinks)
  }
})
</script>

<style scoped>
.modal-toggle-wrapper {
  display: flex;
  align-items: center;
  gap: 12px;
}

.modal-toggle-divider {
  width: 1px;
  height: 24px;
  background-color: var(--vp-c-divider);
}

.modal-toggle {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  cursor: pointer;
  transition: color 0.25s, background-color 0.25s;
  color: var(--vp-c-text-2);
}

.modal-toggle:hover {
  color: var(--vp-c-text-1);
  background-color: var(--vp-c-bg-soft);
}

.toggle-icon {
  width: 18px;
  height: 18px;
}
</style>
