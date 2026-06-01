<template>
  <div ref="toggleRef" class="modal-toggle-wrapper">
    <div class="modal-toggle" @click="toggle" :title="showModal ? '当前：弹窗打开文章，点击切换为直接跳转' : '当前：直接跳转文章，点击切换为弹窗打开'">
      <svg v-if="showModal" class="toggle-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <rect x="2" y="3" width="20" height="14" rx="2" ry="2"></rect>
        <line x1="8" y1="21" x2="16" y2="21"></line>
        <line x1="12" y1="17" x2="12" y2="21"></line>
      </svg>
      <svg v-else class="toggle-icon" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg">
        <path d="M640 469.333333m-42.666667 0a42.666667 42.666667 0 1 0 85.333334 0 42.666667 42.666667 0 1 0-85.333334 0Z" fill="currentColor"></path>
        <path d="M512 469.333333m-42.666667 0a42.666667 42.666667 0 1 0 85.333334 0 42.666667 42.666667 0 1 0-85.333334 0Z" fill="currentColor"></path>
        <path d="M384 469.333333m-42.666667 0a42.666667 42.666667 0 1 0 85.333334 0 42.666667 42.666667 0 1 0-85.333334 0Z" fill="currentColor"></path>
        <path d="M896 0h-597.333333C230.4 0 170.666667 59.733333 170.666667 128V256h-42.666667C59.733333 256 0 315.733333 0 384v512c0 68.266667 59.733333 128 128 128h597.333333c68.266667 0 128-59.733333 128-128V768h42.666667c68.266667 0 128-59.733333 128-128v-512c0-68.266667-59.733333-128-128-128zM768 896c0 25.6-17.066667 42.666667-42.666667 42.666667h-597.333333c-25.6 0-42.666667-17.066667-42.666667-42.666667v-512c0-25.6 17.066667-42.666667 42.666667-42.666667h597.333333c25.6 0 42.666667 17.066667 42.666667 42.666667v512z m170.666667-256c0 25.6-17.066667 42.666667-42.666667 42.666667H853.333333V384C853.333333 315.733333 793.6 256 725.333333 256H256V128c0-25.6 17.066667-42.666667 42.666667-42.666667h597.333333c25.6 0 42.666667 17.066667 42.666667 42.666667v512z" fill="currentColor"></path>
      </svg>
    </div>
    <span class="modal-toggle-divider"></span>
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
  margin-left: 10px;
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
