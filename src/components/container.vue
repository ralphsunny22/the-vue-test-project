<template>
    <div class="container container-drag-box" :style="{ top: position.y + 'px', left: position.x + 'px' }" @mousedown="startDrag">
        <span class="label">Container Box</span>
        <ContentDragBox :disableContainer="disableContainer" @customEvent="handleCustomEvent"/>
    </div>
</template>

<script lang='ts'>
    import { defineComponent, ref } from 'vue';
    import ContentDragBox from './content.vue';

    export default defineComponent({
        name: 'ContainerDragBox',
        components: {
            ContentDragBox,
        },
        setup() {
            const disableContainer = ref(false);
            const position = ref({ x: 0, y: 0 });
            let startX = 0;
            let startY = 0;
            let isDragging = false;

            const startDrag = (event: MouseEvent) => {
                isDragging = true;
                startX = event.clientX - position.value.x;
                startY = event.clientY - position.value.y;

                document.addEventListener('mousemove', handleDrag);
                document.addEventListener('mouseup', stopDrag);
            };

            const handleDrag = (event: MouseEvent) => {
                if (!isDragging) return;

                position.value.x = event.clientX - startX;
                position.value.y = event.clientY - startY;
            };

            const stopDrag = () => {
                isDragging = false;
                document.removeEventListener('mousemove', handleDrag);
                document.removeEventListener('mouseup', stopDrag);
            };

            const handleCustomEvent = () => {
                stopDrag;
            };

            return {
                position,
                startDrag,
                disableContainer,
                handleCustomEvent
            };
        }
    });
</script>




<style lang='postcss' scoped>
    .container {
        @apply w-96 h-80 bg-gray-300 flex items-center justify-center relative;
    }

    .label {
       @apply absolute -top-3 px-3 left-0 bg-gray-300 text-black text-xs;
    }

    .container-drag-box {
        position: relative;
        cursor: move;
      }
</style>