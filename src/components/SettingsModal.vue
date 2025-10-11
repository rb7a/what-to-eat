<template>
    <div v-if="isVisible" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
        <div class="bg-white rounded-lg max-w-2xl w-full mx-4 max-h-[90vh] flex flex-col">
            <!-- 固定头部 -->
            <div class="flex justify-between items-center p-6 pb-4 border-b">
                <h2 class="text-2xl font-bold text-gray-800">系统设置</h2>
                <button @click="closeModal" class="text-gray-500 hover:text-gray-700">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                    </svg>
                </button>
            </div>

            <!-- 可滚动内容区域 -->
            <div class="flex-1 overflow-y-auto px-6 py-4">
                <div class="space-y-6">
                    <!-- 302.AI 推荐广告 -->
                    <div class="bg-gradient-to-r from-blue-50 to-purple-50 border border-blue-200 rounded-lg p-3">
                        <div class="flex items-center gap-3">
                            <div class="flex-shrink-0">
                                <div class="w-10 h-10 from-blue-500 to-purple-600 rounded-xl flex items-center justify-center">
                                    <img src="/logo.svg" alt="302.AI Logo" class="w-12 h-12" />
                                </div>
                            </div>
                            <div class="flex-1">
                                <h3 class="text-base font-semibold text-gray-800 mb-1">🚀 推荐API服务商</h3>
                                <p class="text-xs text-gray-600 mb-2">
                                    本项目正在使用 <strong>302.AI</strong> 提供的高质量AI API服务！<strong>302.AI</strong>
                                    是一个按用量付费的企业级AI资源平台，提供市场上最新、最全面的AI模型和API，以及多种开箱即用的在线AI应用
                                </p>
                                <div class="flex items-center gap-2">
                                    <div class="flex flex-wrap gap-1">
                                        <span class="bg-green-100 text-green-800 text-xs px-2 py-0.5 rounded">✓ 多模型</span>
                                        <span class="bg-green-100 text-green-800 text-xs px-2 py-0.5 rounded">✓ 优惠</span>
                                        <span class="bg-green-100 text-green-800 text-xs px-2 py-0.5 rounded">✓ 稳定</span>
                                    </div>
                                    <a
                                        href="https://share.302.AI/DymMSI"
                                        target="_blank"
                                        class="inline-flex items-center gap-1 bg-blue-500 hover:bg-blue-600 text-white text-xs px-3 py-1 rounded transition-colors ml-auto"
                                    >
                                        <span>访问</span>
                                        <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                            <path
                                                stroke-linecap="round"
                                                stroke-linejoin="round"
                                                stroke-width="2"
                                                d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"
                                            ></path>
                                        </svg>
                                    </a>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- 菜谱生成模型配置 -->
                    <div class="border rounded-lg">
                        <button
                            @click="isTextConfigExpanded = !isTextConfigExpanded"
                            class="w-full p-4 flex items-center justify-between text-left hover:bg-gray-50 transition-colors"
                        >
                            <h3 class="text-lg font-semibold text-gray-800 flex items-center">
                                <svg class="w-5 h-5 mr-2 text-blue-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"
                                    ></path>
                                </svg>
                                菜谱生成模型配置
                            </h3>
                            <svg
                                class="w-5 h-5 text-gray-500 transition-transform"
                                :class="{ 'rotate-180': isTextConfigExpanded }"
                                fill="none"
                                stroke="currentColor"
                                viewBox="0 0 24 24"
                            >
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                            </svg>
                        </button>

                        <div v-show="isTextConfigExpanded" class="px-4 pb-4">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                <div>
                                    <label class="block text-sm font-medium text-gray-700 mb-1">API地址</label>
                                    <input
                                        v-model="textConfig.baseUrl"
                                        type="text"
                                        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                                        placeholder="https://api.example.com/v1/"
                                    />
                                </div>

                                <div>
                                    <label class="block text-sm font-medium text-gray-700 mb-1">API密钥</label>
                                    <input
                                        v-model="textConfig.apiKey"
                                        type="password"
                                        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                                        placeholder="输入API密钥"
                                    />
                                </div>

                                <div>
                                    <label class="block text-sm font-medium text-gray-700 mb-1">模型名称</label>
                                    <input
                                        v-model="textConfig.model"
                                        type="text"
                                        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                                        placeholder="yi-lightning"
                                    />
                                </div>

                                <div>
                                    <label class="block text-sm font-medium text-gray-700 mb-1">温度参数 (0-1)</label>
                                    <input
                                        v-model.number="textConfig.temperature"
                                        type="number"
                                        min="0"
                                        max="1"
                                        step="0.1"
                                        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                                    />
                                </div>

                                <div class="md:col-span-2">
                                    <label class="block text-sm font-medium text-gray-700 mb-1">超时时间 (毫秒)</label>
                                    <input
                                        v-model.number="textConfig.timeout"
                                        type="number"
                                        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500"
                                        placeholder="300000"
                                    />
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- 图片生成模型配置 -->
                    <div class="border rounded-lg">
                        <button
                            @click="isImageConfigExpanded = !isImageConfigExpanded"
                            class="w-full p-4 flex items-center justify-between text-left hover:bg-gray-50 transition-colors"
                        >
                            <h3 class="text-lg font-semibold text-gray-800 flex items-center">
                                <svg class="w-5 h-5 mr-2 text-green-500" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M4 16l4.586-4.586a2 2 0 012.828 0L16 16m-2-2l1.586-1.586a2 2 0 012.828 0L20 14m-6-6h.01M6 20h12a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z"
                                    ></path>
                                </svg>
                                图片生成模型配置
                            </h3>
                            <svg
                                class="w-5 h-5 text-gray-500 transition-transform"
                                :class="{ 'rotate-180': isImageConfigExpanded }"
                                fill="none"
                                stroke="currentColor"
                                viewBox="0 0 24 24"
                            >
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                            </svg>
                        </button>

                        <div v-show="isImageConfigExpanded" class="px-4 pb-4">
                            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                <div>
                                    <label class="block text-sm font-medium text-gray-700 mb-1">API地址</label>
                                    <input
                                        v-model="imageConfig.baseUrl"
                                        type="text"
                                        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500"
                                        placeholder="https://api.example.com/v4/"
                                    />
                                </div>

                                <div>
                                    <label class="block text-sm font-medium text-gray-700 mb-1">API密钥</label>
                                    <input
                                        v-model="imageConfig.apiKey"
                                        type="password"
                                        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500"
                                        placeholder="输入API密钥"
                                    />
                                </div>

                                <div class="md:col-span-2">
                                    <label class="block text-sm font-medium text-gray-700 mb-1">模型名称</label>
                                    <input
                                        v-model="imageConfig.model"
                                        type="text"
                                        class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-green-500"
                                        placeholder="cogview-3-flash"
                                    />
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 固定底部按钮 -->
            <div class="flex justify-end space-x-3 p-6 pt-4 border-t bg-gray-50 rounded-b-lg">
                <button @click="resetToDefault" class="px-4 py-2 text-gray-600 border border-gray-300 rounded-md hover:bg-gray-50 transition-colors">恢复默认</button>
                <button @click="closeModal" class="px-4 py-2 text-gray-600 border border-gray-300 rounded-md hover:bg-gray-50 transition-colors">取消</button>
                <button @click="saveSettings" class="px-4 py-2 bg-blue-500 text-white rounded-md hover:bg-blue-600 transition-colors">保存设置</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive, watch } from 'vue'
import { useSettingsStore } from '../stores/settings'

const props = defineProps({
    isVisible: {
        type: Boolean,
        default: false
    }
})

const emit = defineEmits(['close', 'save'])

const settingsStore = useSettingsStore()

// 折叠状态
const isTextConfigExpanded = ref(false)
const isImageConfigExpanded = ref(false)

// 文本生成配置
const textConfig = reactive({
    baseUrl: '',
    apiKey: '',
    model: '',
    temperature: 0.7,
    timeout: 300000
})

// 图片生成配置
const imageConfig = reactive({
    baseUrl: '',
    apiKey: '',
    model: ''
})

// 监听弹窗显示状态，加载当前配置
watch(
    () => props.isVisible,
    visible => {
        if (visible) {
            loadCurrentSettings()
        }
    }
)

// 加载当前设置
const loadCurrentSettings = () => {
    const settings = settingsStore.getSettings()

    // 加载文本生成配置
    textConfig.baseUrl = settings.textGeneration.baseUrl
    textConfig.apiKey = settings.textGeneration.apiKey
    textConfig.model = settings.textGeneration.model
    textConfig.temperature = settings.textGeneration.temperature
    textConfig.timeout = settings.textGeneration.timeout

    // 加载图片生成配置
    imageConfig.baseUrl = settings.imageGeneration.baseUrl
    imageConfig.apiKey = settings.imageGeneration.apiKey
    imageConfig.model = settings.imageGeneration.model
}

// 保存设置
const saveSettings = () => {
    const newSettings = {
        textGeneration: {
            baseUrl: textConfig.baseUrl,
            apiKey: textConfig.apiKey,
            model: textConfig.model,
            temperature: textConfig.temperature,
            timeout: textConfig.timeout
        },
        imageGeneration: {
            baseUrl: imageConfig.baseUrl,
            apiKey: imageConfig.apiKey,
            model: imageConfig.model
        }
    }

    settingsStore.updateSettings(newSettings)
    emit('save')
    closeModal()
}

// 恢复默认设置
const resetToDefault = () => {
    settingsStore.resetToDefault()
    loadCurrentSettings()
}

// 关闭弹窗
const closeModal = () => {
    emit('close')
}
</script>
