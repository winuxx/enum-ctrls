<script setup lang="ts">
import { useVModel } from '@vueuse/core'

const props = defineProps({
    options: {
        type: Object,
        required: true,
    },
    value: {
        type: [Number, String],
        default: () => null,
    },
})

const emit = defineEmits(['change', 'update:value'])

const selected = useVModel(props, 'value', emit)

function onChange(val: number) {
    emit('change', val)
}
</script>

<template>
    <n-radio-group v-model:value="selected" @update:value="onChange">
        <template v-for="item in options" :key="item">
            <n-radio v-if="typeof item === 'number'" :value="item">{{ options[item] }}</n-radio>
        </template>
    </n-radio-group>
</template>

<style scoped lang="less"></style>
