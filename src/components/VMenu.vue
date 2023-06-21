<script setup>
import { computed, onMounted, onUnmounted, ref } from 'vue'

const show = ref(false)
const activatorRef = ref()
const contentRef = ref()
const position = ref({
  x: 0,
  y: 0
})

const style = computed(() => ({
  top: `${position.value.y}px`,
  left: `${position.value.x}px`
}))

function onClick(event) {
  let x = event.clientX
  let y = event.clientY

  const [rects] = activatorRef.value?.getClientRects() ?? []

  if (rects) {
    x = rects.x
    y = rects.y + rects.height
  }

  position.value.x = x
  position.value.y = y

  show.value = !show.value
}

function onRef(element) {
  activatorRef.value = element
}

function onClickDom(event) {
  if (event.target === activatorRef.value) {
    return
  }

  if (contentRef.value?.contains(event.target)) {
    return
  }

  show.value = false
}

onMounted(() => {
  document.addEventListener('click', onClickDom)
})

onUnmounted(() => {
  document.removeEventListener('click', onClickDom)
})

const activatorAttrs = {
  ref: onRef,
  onClick
}
</script>
<template>
  <slot name="activator" :attrs="activatorAttrs" />

  <teleport to="body">
    <transition
      enter-active-class="transition duration-200"
      leave-active-class="transition duration-200"
      enter-from-class="opacity-0 translate-y-2"
      leave-to-class="opacity-0 translate-y-2"
    >
      <div ref="contentRef" v-if="show" class="fixed left-0 top-0" :style="style">
        <slot />
      </div>
    </transition>
  </teleport>
</template>
