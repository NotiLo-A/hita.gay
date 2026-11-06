<script setup lang="ts">
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'
import { RouterLink } from 'vue-router'

const isOpen = ref(true)
const isMinimized = ref(false)
const isMaximized = ref(false)
const activeDropdown = ref<string | null>(null)
const selectedTool = ref('pencil')

const windowRef = ref<HTMLElement | null>(null)
const isDragging = ref(false)
const position = ref<{ x: number; y: number } | null>(null)
let dragStartOffset = { x: 0, y: 0 }

const windowStyle = computed(() => {
  if (isMaximized.value) {
    return {}
  }
  if (!position.value) {
    return {}
  }
  return {
    position: 'fixed' as const,
    left: `${position.value.x}px`,
    top: `${position.value.y}px`,
    margin: '0',
    zIndex: '100'
  }
})

function startDrag(event: MouseEvent | TouchEvent) {
  const target = event.target as HTMLElement | null
  if (target?.closest('.title-bar-controls')) return
  if (isMaximized.value) return

  if (!windowRef.value) return
  const rect = windowRef.value.getBoundingClientRect()

  const clientX = 'touches' in event ? event.touches[0].clientX : event.clientX
  const clientY = 'touches' in event ? event.touches[0].clientY : event.clientY

  dragStartOffset = {
    x: clientX - rect.left,
    y: clientY - rect.top
  }

  if (!position.value) {
    position.value = { x: rect.left, y: rect.top }
  }

  isDragging.value = true

  window.addEventListener('mousemove', onDrag)
  window.addEventListener('mouseup', stopDrag)
  window.addEventListener('touchmove', onDrag, { passive: false })
  window.addEventListener('touchend', stopDrag)
}

function onDrag(event: MouseEvent | TouchEvent) {
  if (!isDragging.value || !windowRef.value) return

  const clientX = 'touches' in event ? event.touches[0].clientX : event.clientX
  const clientY = 'touches' in event ? event.touches[0].clientY : event.clientY

  const newX = clientX - dragStartOffset.x
  const newY = Math.max(0, clientY - dragStartOffset.y)

  position.value = {
    x: newX,
    y: newY
  }

  if ('touches' in event) {
    event.preventDefault()
  }
}

function stopDrag() {
  isDragging.value = false
  window.removeEventListener('mousemove', onDrag)
  window.removeEventListener('mouseup', stopDrag)
  window.removeEventListener('touchmove', onDrag)
  window.removeEventListener('touchend', stopDrag)
}

function toggleDropdown(menu: string) {
  activeDropdown.value = activeDropdown.value === menu ? null : menu
}

function closeDropdowns() {
  activeDropdown.value = null
}

function handleGlobalClick(event: MouseEvent) {
  const target = event.target as HTMLElement | null
  if (!target) return
  if (!target.closest('.dropdown')) {
    closeDropdowns()
  }
}

onMounted(() => {
  document.addEventListener('click', handleGlobalClick)
})

onBeforeUnmount(() => {
  document.removeEventListener('click', handleGlobalClick)
  stopDrag()
})
</script>

<template>
  <div class="page-container">
    <button v-if="!isOpen" class="restore-window-btn" @click="isOpen = true">
      <img src="/img/painticon.png" width="16" height="16" alt="Paint icon" />
      <span>HITA - Paint</span>
    </button>

    <div
      v-if="isOpen"
      id="drag"
      ref="windowRef"
      class="window"
      :class="{ 'window-maximized': isMaximized, 'window-dragging': isDragging }"
      :style="windowStyle"
    >
      <div
        id="header4"
        class="title-bar"
        @mousedown="startDrag"
        @touchstart="startDrag"
      >
        <div class="title-bar-text">
          <img src="/img/painticon.png" height="15" alt="Paint icon" />
          HITA - Paint
        </div>
        <div class="title-bar-controls">
          <button
            aria-label="Minimize"
            @click="isMinimized = !isMinimized"
          ></button>
          <button
            aria-label="Maximize"
            @click="isMaximized = !isMaximized"
          ></button>
          <button
            aria-label="Close"
            @click="isOpen = false"
          ></button>
        </div>
      </div>

      <div v-show="!isMinimized" class="window-body">
        <div class="topmenu">
          <div class="dropdown">
            <button
              class="menu-btn"
              :class="{ active: activeDropdown === 'file' }"
              @click.stop="toggleDropdown('file')"
            >
              <u>F</u>ile
            </button>
            <div v-show="activeDropdown === 'file'" class="dropdown-content">
              <a href="#" @click.prevent="closeDropdowns">New</a>
              <a href="#" @click.prevent="closeDropdowns">Open...</a>
              <a href="#" @click.prevent="closeDropdowns">Save</a>
              <hr />
              <a href="#" @click.prevent="isOpen = false">Exit</a>
            </div>
          </div>

          <div class="dropdown">
            <button
              class="menu-btn"
              :class="{ active: activeDropdown === 'edit' }"
              @click.stop="toggleDropdown('edit')"
            >
              <u>E</u>dit
            </button>
            <div v-show="activeDropdown === 'edit'" class="dropdown-content">
              <a href="#" @click.prevent="closeDropdowns">Undo</a>
              <a href="#" @click.prevent="closeDropdowns">Repeat</a>
              <hr />
              <a href="#" @click.prevent="closeDropdowns">Cut</a>
              <a href="#" @click.prevent="closeDropdowns">Copy</a>
              <a href="#" @click.prevent="closeDropdowns">Paste</a>
              <hr />
              <a href="#" @click.prevent="closeDropdowns">Select All</a>
            </div>
          </div>

          <div class="dropdown">
            <button
              class="menu-btn"
              :class="{ active: activeDropdown === 'view' }"
              @click.stop="toggleDropdown('view')"
            >
              <u>V</u>iew
            </button>
            <div v-show="activeDropdown === 'view'" class="dropdown-content">
              <a href="#" @click.prevent="closeDropdowns">Tool Box</a>
              <a href="#" @click.prevent="closeDropdowns">Color Box</a>
              <a href="#" @click.prevent="closeDropdowns">Status Bar</a>
            </div>
          </div>

          <div class="dropdown">
            <button
              class="menu-btn links"
              :class="{ active: activeDropdown === 'links' }"
              @click.stop="toggleDropdown('links')"
            >
              <u>L</u>inks
            </button>
            <div
              v-show="activeDropdown === 'links'"
              class="dropdown-content ldropdown-content"
            >
              <a href="https://github.com/NotiLo-A" target="_blank" rel="noopener noreferrer" @click="closeDropdowns"><u>G</u>itHub</a>
              <a href="https://t.me/hita_u" target="_blank" rel="noopener noreferrer" @click="closeDropdowns"><u>T</u>elegram</a>
              <a href="mailto:ninedefix@proton.me" @click="closeDropdowns"><u>E</u>mail</a>
              <hr />
              <RouterLink to="/me" @click="closeDropdowns"><u>M</u>ore About Me</RouterLink>
            </div>
          </div>
        </div>

        <div class="msbody">
          <div class="msnav">
            <hr class="nav-divider" />
            <div class="navcolumn">
              <div
                :class="selectedTool === 'star' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'star'"
              >
                <img src="/img/mspaint/starthingy.png" alt="star" />
              </div>
              <div
                :class="selectedTool === 'box' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'box'"
              >
                <img src="/img/mspaint/box.png" alt="box" />
              </div>
            </div>
            <div class="navcolumnrow">
              <div
                :class="selectedTool === 'eraser' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'eraser'"
              >
                <img src="/img/mspaint/eraser.png" alt="eraser" />
              </div>
              <div
                :class="selectedTool === 'paint' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'paint'"
              >
                <img src="/img/mspaint/paint.png" alt="paint" />
              </div>
            </div>
            <div class="navcolumnrow">
              <div
                :class="selectedTool === 'dropper' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'dropper'"
              >
                <img src="/img/mspaint/dropper.png" alt="dropper" />
              </div>
              <div
                :class="selectedTool === 'search' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'search'"
              >
                <img src="/img/mspaint/search.png" alt="search" />
              </div>
            </div>
            <div class="navcolumnrow">
              <div
                :class="selectedTool === 'pencil' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'pencil'"
              >
                <img src="/img/mspaint/pencil.png" alt="pencil" />
              </div>
              <div
                :class="selectedTool === 'brush' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'brush'"
              >
                <img src="/img/mspaint/brush.png" alt="brush" />
              </div>
            </div>
            <div class="navcolumnrow">
              <div
                :class="selectedTool === 'fill' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'fill'"
              >
                <img src="/img/mspaint/fillthing.png" alt="fill" />
              </div>
              <div
                :class="selectedTool === 'type' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'type'"
              >
                <img src="/img/mspaint/type.png" alt="type" />
              </div>
            </div>
            <div class="navcolumnrow">
              <div
                :class="selectedTool === 'line' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'line'"
              >
                <img src="/img/mspaint/line.png" alt="line" />
              </div>
              <div
                :class="selectedTool === 'curve' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'curve'"
              >
                <img src="/img/mspaint/curve.png" alt="curve" />
              </div>
            </div>
            <div class="navcolumnrow">
              <div
                :class="selectedTool === 'box2' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'box2'"
              >
                <img src="/img/mspaint/box2.png" alt="box2" />
              </div>
              <div
                :class="selectedTool === 'weridshit' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'weridshit'"
              >
                <img src="/img/mspaint/weridshit.png" alt="select" />
              </div>
            </div>
            <div class="navcolumnrow">
              <div
                :class="selectedTool === 'oval' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'oval'"
              >
                <img src="/img/mspaint/oval.png" alt="oval" />
              </div>
              <div
                :class="selectedTool === 'oval2' ? 'navbuttonsactive' : 'navbuttons'"
                @click="selectedTool = 'oval2'"
              >
                <img src="/img/mspaint/oval2.png" alt="oval2" />
              </div>
            </div>
            <div class="emptyboxfordecorationiguess"></div>
            <hr class="nav-divider-bottom" />
          </div>

          <div class="main"></div>
        </div>

        <div class="msfooter">
          <img class="colors" src="/img/paintcolors.png" alt="paint colors" />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@font-face {
  font-family: 'PixelOperator';
  src: url('/fonts/PixelOperator.ttf') format('truetype');
  font-weight: normal;
  font-style: normal;
}

.page-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 1.5rem 1rem 1rem;
  background-image: url('/img/background.png');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  background-repeat: no-repeat;
  box-sizing: border-box;
}

.restore-window-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  font-family: 'PixelOperator', sans-serif;
  font-size: 16px;
  cursor: pointer;
  margin: auto;
}

.window {
  background: silver;
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #dfdfdf, inset -2px -2px grey, inset 2px 2px #fff;
  padding: 3px;
  max-width: 960px;
  width: 100%;
  font-family: 'PixelOperator', sans-serif;
  color: #000;
  box-sizing: border-box;
  margin: auto auto 1.5rem;
}

.window-maximized {
  max-width: 100% !important;
  width: 100% !important;
}

#header4 {
  font-size: 20px;
}

.title-bar {
  align-items: center;
  background: linear-gradient(
    90deg,
    #ce2e37,
    #d2771e,
    #d4cb1f,
    #81c220,
    #21a184,
    #2582b5,
    #8f289f,
    #bd2f68,
    #ce2e37,
    #d2771e,
    #d4cb1f,
    #81c220,
    #21a184,
    #2582b5,
    #8f289f,
    #bd2f68,
    #ce2e37
  );
  background-size: 200% 100%;
  animation: rainbow-flow 5s linear infinite;
  display: flex;
  justify-content: space-between;
  padding: 3px 2px 3px 3px;
  cursor: grab;
  user-select: none;
}

@keyframes rainbow-flow {
  0% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

@media (prefers-reduced-motion: reduce) {
  .title-bar {
    animation: none;
  }
}

.window-dragging .title-bar {
  cursor: grabbing;
}

.title-bar-text {
  color: #fff;
  font-weight: 700;
  letter-spacing: 0;
  margin-right: 24px;
  display: flex;
  align-items: center;
  gap: 4px;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.7);
  pointer-events: none;
}

.title-bar-controls {
  display: flex;
  cursor: default;
}

.title-bar-controls button {
  display: block;
  min-height: 14px;
  min-width: 16px;
  padding: 0;
  background: silver;
  border: none;
  border-radius: 0;
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #fff, inset -2px -2px grey, inset 2px 2px #dfdfdf;
  box-sizing: border-box;
  cursor: pointer;
}

.title-bar-controls button:active {
  box-shadow: inset -1px -1px #fff, inset 1px 1px #0a0a0a, inset -2px -2px #dfdfdf, inset 2px 2px grey;
}

.title-bar-controls button:focus {
  outline: none;
}

.title-bar-controls button[aria-label=Minimize] {
  background-image: url("data:image/svg+xml;charset=utf-8,%3Csvg width='6' height='2' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath fill='%23000' d='M0 0h6v2H0z'/%3E%3C/svg%3E");
  background-position: bottom 3px left 4px;
  background-repeat: no-repeat;
}

.title-bar-controls button[aria-label=Maximize] {
  background-image: url("data:image/svg+xml;charset=utf-8,%3Csvg width='9' height='9' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath fill-rule='evenodd' clip-rule='evenodd' d='M9 0H0v9h9V0zM8 2H1v6h7V2z' fill='%23000'/%3E%3C/svg%3E");
  background-position: top 2px left 3px;
  background-repeat: no-repeat;
}

.title-bar-controls button[aria-label=Close] {
  background-image: url("data:image/svg+xml;charset=utf-8,%3Csvg width='8' height='7' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath fill-rule='evenodd' clip-rule='evenodd' d='M0 0h2v1h1v1h2V1h1V0h2v1H7v1H6v1H5v1h1v1h1v1h1v1H6V6H5V5H3v1H2v1H0V6h1V5h1V4h1V3H2V2H1V1H0V0z' fill='%23000'/%3E%3C/svg%3E");
  background-position: top 2px left 3px;
  background-repeat: no-repeat;
  margin-left: 2px;
}

.window-body {
  margin: 8px;
}

.topmenu {
  margin-left: 20px;
  font-size: 18px;
  display: flex;
  align-items: center;
  margin-top: -3px;
  margin-bottom: 5px;
  font-family: 'PixelOperator', sans-serif;
  gap: 2px;
}

.dropdown {
  position: relative;
  z-index: 20;
}

.menu-btn {
  background: silver;
  border: none;
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #ffffff, inset -2px -2px grey, inset 2px 2px #fff;
  padding: 2px 8px 3px 8px;
  font-family: 'PixelOperator', sans-serif;
  font-size: 18px;
  line-height: 90%;
  color: #000;
  cursor: pointer;
  box-sizing: border-box;
  user-select: none;
  position: relative;
}

.menu-btn:hover,
.menu-btn:active,
.menu-btn.active {
  box-shadow: inset -1px -1px #fff, inset 1px 1px #0a0a0a, inset -2px -2px #dfdfdf, inset 2px 2px grey;
  background: #c0c0c0;
}

.menu-btn:focus {
  outline: none;
}

.dropdown-content {
  position: absolute;
  top: 24px;
  left: 0;
  background: silver;
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #dfdfdf, inset -2px -2px grey, inset 2px 2px #fff;
  z-index: 50;
  min-width: 120px;
}

.sdropdown-content {
  width: 200px;
}

.ldropdown-content {
  width: 140px;
}

.dropdown-content a {
  color: black;
  margin: 2px;
  padding: 4px 8px;
  text-decoration: none;
  display: block;
  font-family: 'PixelOperator', sans-serif;
  font-size: 16px;
  white-space: nowrap;
}

.dropdown-content a:hover {
  background-image: linear-gradient(to right, #ce2e37, #d2771e, #d4cb1f, #81c220, #21a184, #2582b5);
  color: white;
}

.dropdown hr {
  border: none;
  border-top: 2px solid darkgray;
  border-bottom: 2px solid white;
  width: 95%;
  margin: 2px auto;
}

.msbody {
  display: flex;
}

.msnav {
  margin: 5px 5px 5px 15px;
  flex-shrink: 0;
}

.nav-divider {
  width: 120%;
  margin-left: -12px;
  margin-top: -5px;
  margin-bottom: -5px;
  border: none;
  border-top: 2px solid darkgray;
  border-bottom: 2px solid white;
}

.nav-divider-bottom {
  width: 120%;
  margin-left: -12px;
  margin-top: 17px;
  margin-bottom: -5px;
  border: none;
  border-top: 2px solid darkgray;
  border-bottom: 2px solid white;
}

.navcolumn {
  width: 75px;
  margin-top: 5px;
  display: flex;
}

.navcolumnrow {
  display: flex;
}

.navbuttons,
.navbuttonsactive {
  width: 37px;
  height: 35px;
  background: rgb(204, 203, 203);
  text-align: center;
  padding-top: 2px;
  box-sizing: border-box;
  cursor: pointer;
  user-select: none;
}

.navbuttons {
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #ffffff, inset -2px -2px grey, inset 2px 2px #fff;
}

.navbuttons:hover {
  background-image: url(/img/mspaint/buttonbg.png);
  background-size: contain;
  box-shadow: inset -1px -1px #0a0a0a, inset 1px 1px #000000, inset -2px -2px grey, inset 2px 2px #000000;
}

.navbuttons:active,
.navbuttonsactive {
  background-image: url(/img/mspaint/buttonbg.png);
  background-size: contain;
  box-shadow: inset -1px -1px #fff, inset 1px 1px #0a0a0a, inset -2px -2px #dfdfdf, inset 2px 2px grey;
}

.navbuttons img,
.navbuttonsactive img {
  width: 33px;
  text-align: center;
  pointer-events: none;
}

.emptyboxfordecorationiguess {
  width: 60px;
  height: 210px;
  border: 2px inset white;
  margin-top: 5px;
  margin-left: auto;
  margin-right: auto;
}

.main {
  background-color: white;
  background-image: url('/img/paint-canvas.jpg?v=2');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  color: black;
  padding: 20px;
  margin-right: 10px;
  height: 520px;
  overflow: auto;
  overflow-x: hidden;
  border: 2px groove transparent;
  border-image: url("data:image/svg+xml;charset=utf-8,%3Csvg width='5' height='5' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath fill='gray' d='M0 0h4v1H0z'/%3E%3Cpath fill='gray' d='M0 0h1v4H0z'/%3E%3Cpath fill='%230a0a0a' d='M1 1h2v1H1z'/%3E%3Cpath fill='%230a0a0a' d='M1 1h1v2H1z'/%3E%3Cpath fill='%23fff' d='M0 4h5v1H0z'/%3E%3Cpath fill='%23fff' d='M4 0h1v5H4z'/%3E%3Cpath fill='%23dfdfdf' d='M3 1h1v3H3z'/%3E%3Cpath fill='%23dfdfdf' d='M1 3h3v1H1z'/%3E%3C/svg%3E") 2;
  position: relative;
  flex: 1;
}

.msfooter {
  position: relative;
}

.colors {
  margin-left: 50px;
  margin-top: 10px;
  height: 40px;
}

u {
  text-decoration: underline;
}
</style>
