<script setup lang="ts">
import { useVModel } from '@vueuse/core'

const props = defineProps({
    options: {
        type: Object,
        required: true,
    },
    value: {
        type: Array,
        default: () => [],
    },
})

const emit = defineEmits(['change', 'update:value'])

const selected = useVModel(props, 'value', emit) as any

function onChange(val: number[]) {
    emit('change', val)
}
</script>

<template>
    <n-checkbox-group v-model:value="selected" @update:value="onChange">
        <template v-for="item in options" :key="item">
            <n-checkbox v-if="typeof item === 'number'" :value="item" :label="options[item]" />
        </template>
    </n-checkbox-group>
</template>

<style scoped lang="less"></style>
