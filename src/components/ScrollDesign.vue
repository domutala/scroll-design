<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref, getCurrentInstance } from 'vue'

defineProps({ lineColor: { type: String } })

const isVisible = ref(false)
const instance = getCurrentInstance()
const lineHeight = ref(0)

onMounted(mounted)
function mounted() {
  addEventListener('scroll', scroll)
  addEventListener('resize', setHeight)
  addEventListener('scroll-design', (e) => onVisible(e as any))
  setHeight()
  scroll()
}

function onVisible(e: CustomEvent) {
  if (!instance?.proxy) return

  const $el = instance.proxy.$el as HTMLDivElement
  const brothers = $el.parentElement!.querySelectorAll('.scroll-design')

  let index = 0
  brothers.forEach((child, i) => {
    if (child === $el) index = i
  })

  if (index !== e.detail.index) scroll()
}

function setHeight() {
  lineHeight.value = 0
  if (!instance?.proxy) return
  const $el = instance.proxy.$el as HTMLDivElement
  lineHeight.value = $el.getBoundingClientRect().height
}

function scroll() {
  if (!instance?.proxy) return

  const $el = instance.proxy.$el as HTMLDivElement
  const rect = $el.getBoundingClientRect()
  const viewportHeight = window.innerHeight
  const brothers = $el.parentElement!.querySelectorAll('.scroll-design')

  let index = 0
  brothers.forEach((child, i) => {
    if (child === $el) index = i
  })

  if ($el.getAttribute('visible') !== null) {
    const isntV = rect.top < viewportHeight * 0.75
    if (isntV) return

    const cadet = brothers.item(index + 1)
    if (cadet && cadet.getAttribute('visible') !== null) return

    isVisible.value = false
    setTimeout(() => {
      $el.removeAttribute('visible')
      window.dispatchEvent(
        new CustomEvent('scroll-design', { detail: { index, visible: isVisible.value } })
      )
    }, 500)
  } else {
    // si l'élément est visible dans l'écran
    const isV = rect.top < viewportHeight * 0.5
    if (!isV) return

    const elder = brothers.item(index - 1)
    if (elder && elder.getAttribute('visible') === null) return

    isVisible.value = true
    setTimeout(() => {
      $el.setAttribute('visible', '')
      dispatchEvent(
        new CustomEvent('scroll-design', { detail: { index, visible: isVisible.value } })
      )
    }, 500)
  }
}

onBeforeUnmount(destroy)
function destroy() {
  removeEventListener('resize', setHeight)
  removeEventListener('scroll', scroll)
  removeEventListener('scroll-design', (e) => onVisible(e as any))
}
</script>

<template>
  <div class="scroll-design" :class="{ visible: !isVisible }">
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
