<template>
    <div class="wrap">
        <div class="brandfilter">
            <span class="brand" v-for="(item, key) in data" :key="key">
                <a class="a" :href="withBase(`/?brand=${String(key)}`)" @click="closeDropdown"> {{ key }}<strong class="VPBadge tip strong mini">{{
                    data[key].length }}</strong></a>
            </span>
        </div>
    </div>
</template>
<script lang="ts" setup>
import { computed } from 'vue'
import { withBase } from 'vitepress'
import { initBrandFilter } from '../functions'
import { data as themeposts } from '../posts.data'
const data = computed(() => initBrandFilter(themeposts))

function closeDropdown(event: Event) {
    let element = event.target as HTMLElement
    while (element && !element.classList.contains('wrap')) {
        element = element.parentElement as HTMLElement
    }
    if (element) {
        const brandfilterButton = document.querySelector('.brandfilter-btn.a')
        if (brandfilterButton) {
            brandfilterButton.click()
        }
    }
}
</script>

<style scoped>
.wrap {
    min-width: 300px;
    min-height: 100px;
    max-height: 40vh;
    max-width: 40vw;
    overflow-y: auto;
    padding: 20px;
}

.brandfilter {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    line-height: 24px;
}

.brand {
    margin: 5px;
    padding: 0 8px;
    display: inline-block;
    background-color: rgba(123, 123, 123, .05);
    color: var(--vp-c-text-1);
    font-size: 12px;
    border-radius: 2px;
    line-height: 24px;

    .a {
        color: var(--vp-c-text-1);
        font-weight: 500;
        text-decoration: none;
    }

    .a:hover {
        color: var(--vp-c-brand);
    }
}
</style>
