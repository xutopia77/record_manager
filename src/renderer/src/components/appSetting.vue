<template>
    <div class="app-setting-container">
        <div class="setting-card">
            <h3 class="setting-title">程序设置</h3>
            <div class="mode-selector">
                <span class="option-label">界面语言:</span>
                <select v-model="selectedLanguage" class="xc-select">
                    <option value="zh-CN">中文</option>
                    <option value="en-US">English</option>
                </select>
            </div>
        </div>

        <div class="setting-card">
            <h3 class="setting-title">操作</h3>
            <button class="xc-button primary" @click="btnclk_saveSettings">保存设置</button>
            <button class="xc-button" @click="btnclk_resetSettings">恢复默认</button>
        </div>
    </div>
</template>

<script lang="ts" setup>
import { onMounted, ref } from 'vue'
import '@renderer/assets/common.css'
// import { IpcApi } from '../utils/ipcApi'
import * as Dty from '../../../bridge/dataTypedef'
import { useAppStore } from '@renderer/stores/AppStore'
const appStore = useAppStore()
// import util from '@renderer/utils/util'

const selectedLanguage = ref<Dty.LangType>('zh-CN')

async function btnclk_saveSettings(): Promise<void> {
    // todo  is need optimize
    console.log(`save set`)
    appStore.prj.language = selectedLanguage.value
    localStorage.setItem('locale', appStore.prj.language)
    window.location.reload()
    return
}

async function btnclk_resetSettings(): Promise<void> {
    // todo  is need optimize
    console.log(`reset set`)
    appStore.prj.language = 'zh-CN'
}

// ------------------------------------------------

onMounted(() => {})
</script>

<style scoped>
.app-setting-container {
    height: 100%;
    width: 100%;
    padding: 15px;
    margin: 0;
    background-color: var(--xc-background-color);
    color: var(--xc-text-color);
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    display: flex;
    flex-direction: column;
    gap: 12px;
    overflow: hidden;
    box-sizing: border-box;
}

.setting-card {
    background-color: #2d2d30;
    border: 1px solid #444;
    border-radius: 6px;
    padding: 12px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
    flex-shrink: 0;
}

.setting-title {
    margin: 0 0 10px 0;
    padding-bottom: 6px;
    border-bottom: 1px solid #444;
    color: #ddd;
    font-size: 15px;
    font-weight: 600;
}

.mode-selector {
    display: flex;
    align-items: center;
    gap: 8px;
}

.option-label {
    color: #ccc;
    font-size: 13px;
}
</style>
