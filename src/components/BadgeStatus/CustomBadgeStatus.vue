<template>
    <Ellipsis  placement="topLeft" style="max-width:80px;">
        <span class="dot" :style="{ backgroundColor: _color}"></span>
        <span>{{ text }}</span>
    </Ellipsis>
</template>

<script setup lang="ts">
// import { StatusColorEnum } from '@/utils/consts.ts';
import { getHexColor } from './color'
const props = defineProps({
    text: {
        type: String,
    },
    status: {
        type: [String, Number],
        default: 'default',
        // validator: (value) => {
        //     // 这个值必须匹配下列字符串中的一个
        //     return Object.keys(StatusColorEnum).includes(value);
        // },
    },
    /**
     * 自定义status值颜色
     * @example {
     *   1: 'success',
     *   0: 'error'
     * }
     */
    statusNames: {
      type: Object,
      default: () => ({
        'success': 'success',
        'warning': 'warning',
        'error': 'error',
        'default': 'default',
      })
    },
});

const _color = computed(() => {
  return getHexColor(props.statusNames[props.status], 1)
})
</script>
<style lang="less" scoped>
.dot{
    display: inline-block;
    width: 6px;
    height: 6px;
    border-radius: 50%;
    margin: 0 10px
}
</style>
