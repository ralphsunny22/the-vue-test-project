<template>
   <div class="container content-drag-box" :style="{ top: position.y + 'px', left: position.x + 'px' }" @mousedown="startDrag">
      <span class="label">Content drag Boxx</span>
   </div>
</template>

<script lang='ts'>
import { defineComponent, ref, PropType } from 'vue';

export default defineComponent({
        name: 'ContentDragBox',
        props: {
               disableContainer: {
                  type: Boolean as PropType<boolean>,
                  required: true
      
               },
            },
        
        setup() {
            
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

            return {
                position,
                startDrag,
            };
        }
    });
    
</script>

<style lang='postcss' scoped>
   .container  {
      @apply bg-black h-24 w-36 relative;
   }
 .label {
       @apply absolute -top-3 px-3 left-0 bg-black text-white text-xs
    }
.container-drag-box {
      position: absolute;
      cursor: move;
    }
</style>