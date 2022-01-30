<script setup lang="ts">
// import { ref } from 'vue'
import { useVModel } from '@vueuse/core'
import useEnumOptions from './enum-options'

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

const _options = useEnumOptions(props.options)

const selected = useVModel(props, 'value', emit)

function onChange(val: number) {
    emit('change', val)
}
</script>

<template>
    <n-select
        v-model:value="selected"
        v-bind="$attrs"
        :options="_options"
        @update:value="onChange"
    />
</template>

<style scoped lang="less"></style>
