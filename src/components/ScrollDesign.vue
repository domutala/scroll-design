<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref, getCurrentInstance } from 'vue'

defineProps({ lineColor: { type: String } })

const isVisible = ref(false)
const instance = getCurrentInstance()
const lineHeight = ref(0)

window.addEventListener('scroll', scroll)

onMounted(setHeight)
function setHeight() {
  if (!instance?.proxy) return
  const $el = instance.proxy.$el as HTMLDivElement
  lineHeight.value = $el.getBoundingClientRect().height
}

onMounted(scroll)
function scroll() {
  if (!instance?.proxy) return

  const $el = instance.proxy.$el as HTMLDivElement
  const rect = $el.getBoundingClientRect()
  const viewportHeight = window.innerHeight

  const brothers = $el.parentElement!.querySelectorAll(
    '.scroll-design'
  ) as NodeListOf<HTMLDivElement>

  let index = 0
  let is = false

  brothers.forEach((child, i) => {
    if (child === $el) index = i
  })

  if (brothers.item(index - 1)) {
    if (brothers.item(index - 1).getAttribute('visible') === 'true') {
      is = isVisible.value = rect.top < viewportHeight * 0.7
    }
  } else is = isVisible.value = rect.top < viewportHeight * 0.5

  isVisible.value = is
}

onBeforeUnmount(destroy)
function destroy() {
  window.removeEventListener('scroll', scroll)
}
</script>

<template>
  <div class="scroll-design" :visible="isVisible" :class="{ visible: !isVisible }">
    <div class="sd-line">
      <div>
        <transition enter-active-class="animate-in" leave-active-class="animate-out">
          <div v-if="isVisible">
            <div :style="{ background: lineColor, height: `${lineHeight}px` }"></div>
          </div>
        </transition>
      </div>
    </div>
    <div class="sd-container">
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt optio
      blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis hic
      ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.Lorem ipsum dolor sit amet consectetur, adipisicing elit. Dolorem, minus. Nesciunt
      optio blanditiis in perferendis aperiam enim pariatur, est reprehenderit cum placeat corporis
      hic ullam debitis, explicabo modi dolorem veritatis.Lorem ipsum dolor sit amet consectetur,
      adipisicing elit. Dolorem, minus. Nesciunt optio blanditiis in perferendis aperiam enim
      pariatur, est reprehenderit cum placeat corporis hic ullam debitis, explicabo modi dolorem
      veritatis.
    </div>
  </div>
</template>

<style lang="scss" scoped>
.scroll-design {
  display: flex;

  .sd-line {
    > * {
      height: 100%;
      width: 5px;
      overflow: hidden;

      > * {
        width: 100%;
        animation-duration: 0.5s;
        animation-fill-mode: both;
        overflow: hidden;

        > * {
          width: 100%;
        }

        &.animate-in {
          @keyframes animate-in {
            0% {
              height: 0;
            }
            100% {
              height: 100%;
            }
          }

          animation-name: animate-in;
        }

        &.animate-out {
          @keyframes animate-out {
            0% {
              height: 100%;
            }
            100% {
              height: 0;
            }
          }

          animation-name: animate-out;
        }
      }
    }
  }
}
</style>
