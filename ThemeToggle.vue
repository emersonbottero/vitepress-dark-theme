<template>
  <div class="switch-wrapper">
    <div class="switch-button">
      <input
        ref="toggle"
        class="switch-button-checkbox"
        type="checkbox"
        @click="toggleTheme"
      />
      <label class="switch-button-label" for=""
        ><span class="switch-button-label-span">OS</span></label
      >
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref, watch } from 'vue'
const toggle = ref(null)

/** Set by checkbox */
const currentTheme = ref('')
watch(currentTheme, (currentTheme, _) => {
  const body = document.body
  toggle.value.classList.remove('os')
  body.classList.remove('dark-mode')

  switch (currentTheme) {
    case 'os':
      toggle.value.classList.add('os')

      if (
        window.matchMedia &&
        window.matchMedia('(prefers-color-scheme: dark)').matches
      ) {
        body.classList.add('dark-mode')
      }

      break
    case 'dark':
      body.classList.add('dark-mode')
      break
  }
})

onMounted(() => {
  checkUserPreference()

  //Check OS theme changes when no theme are set
  window
    .matchMedia('(prefers-color-scheme: dark)')
    .addEventListener('change', (e) => {
      const newColorScheme = e.matches ? 'dark' : 'light'
      if (
        localStorage.getItem('dark-theme') === null &&
        localStorage.getItem('light-theme') === null
      )
        if (newColorScheme == 'dark') document.body.classList.add('dark-mode')
        else document.body.classList.remove('dark-mode')
    })
})

const toggleTheme = (e) => {
  let cb = e.target
  const body = document.body

  //Should use OS
  if (cb.readOnly) {
    cb.indeterminate = true
    cb.checked = cb.readOnly = false
    currentTheme.value = 'os'
  } else if (cb.checked) {
    currentTheme.value = 'dark'
  } else {
    currentTheme.value = 'light'
    cb.readOnly = true
  }
  setUserPreferences(currentTheme.value)
}

const checkUserPreference = () => {
  //Check Storage on Page load. Keep user preference through sessions
  const body = document.body

  if (localStorage.getItem('dark-theme')) {
    body.classList.add('dark-mode')
    console.log(toggle.value)
    toggle.value.checked = true
    toggle.value.indeterminate = false
  } else if (localStorage.getItem('light-theme')) {
    body.classList.add('light-mode')
    toggle.value.checked = false
    toggle.value.indeterminate = false
  } else {
    if (!toggle.value.classList.contains('os')) toggle.value.classList.add('os')
    toggle.value.indeterminate = true
    if (
      window.matchMedia &&
      window.matchMedia('(prefers-color-scheme: dark)').matches
    ) {
      body.classList.add('dark-mode')
    } else body.classList.add('light-mode')
  }
}

const setUserPreferences = (currentSelectedTheme) => {
  localStorage.removeItem('light-theme')
  localStorage.removeItem('dark-theme')
  switch (currentSelectedTheme) {
    case 'dark':
      localStorage.setItem('dark-theme', 'true')
      break
    case 'light':
      localStorage.setItem('light-theme', 'true')
      break
  }
}
</script>

<style scoped>
.switch-wrapper {
  padding-left: 24px;
}
.switch-button {
  border: solid 0.5px #a9a9a973;
  background: transparent;
  border-radius: 50px;
  overflow: hidden;
  width: 72px;
  text-align: center;
  height: 24px;
  color: #155fff;
  position: relative;
  padding: 0px;
}
.switch-button:before {
  content: '🔆';
  position: absolute;
  top: 0;
  bottom: 0;
  width: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 3;
  pointer-events: none;
}
.switch-button:after {
  content: '🌙';
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  width: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 3;
  pointer-events: none;
}
.switch-button-checkbox {
  cursor: pointer;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  z-index: 2;
}
.switch-button-checkbox + .switch-button-label:before {
  transform: translateX(-24px);
  transition: transform 300ms linear;
}
.switch-button-checkbox:checked + .switch-button-label:before {
  transform: translateX(24px);
  transition: transform 150ms linear;
}
.switch-button-checkbox + .switch-button-label {
  position: relative;
  display: block;
  user-select: none;
  pointer-events: none;
}
.switch-button-checkbox + .switch-button-label:before {
  content: '';
  line-height: 24px;
  background: #838383;
  height: 24px;
  width: 24px;
  position: absolute;
  border-radius: 50px;
  transform: translateX(-25px);
  transition: transform 300ms;
}
.switch-button-checkbox + .switch-button-label .switch-button-label-span {
  color: gray;
  font-weight: 600;
  position: relative;
}
.switch-button-checkbox.os + .switch-button-label:before {
  transform: translateX(-1px);
  transform: translateY(-1px);
  transition: transform 150ms linear;
}
</style>
