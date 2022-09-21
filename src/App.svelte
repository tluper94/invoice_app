<script lang="ts">
  import Nav from "./lib/Nav.svelte";
  import {onMount, onDestroy} from 'svelte'
  const STORAGE_KEY = 'theme'
  const DARKMODE = '(prefers-color-scheme: dark)'
  let currentTheme:string = localStorage.getItem(STORAGE_KEY)

  const THEMES = {
    DARK: 'dark',
    LIGHT: 'light'
  };

  const prefersDarkTheme = () => window.matchMedia(DARKMODE)

  const applyTheme = () => {
    const preferredTheme = prefersDarkTheme() ? THEMES.DARK: THEMES.LIGHT
    currentTheme = localStorage.getItem(STORAGE_KEY) ?? preferredTheme
    if(currentTheme === THEMES.DARK) {
      document.body.classList.remove(THEMES.LIGHT)
      document.body.classList.add(THEMES.DARK)
    } else {
      document.body.classList.remove(THEMES.DARK)
      document.body.classList.add(THEMES.LIGHT)
    }
  }

  const toggleTheme = () => {
    const stored = localStorage.getItem(STORAGE_KEY)

    if (stored) {
      localStorage.removeItem(STORAGE_KEY)
    } else {
      localStorage.setItem(STORAGE_KEY, prefersDarkTheme() ? THEMES.LIGHT: THEMES.DARK)
    }

    applyTheme()
  }

  const setBodyHeight = () => {
    document.body.style.setProperty('--height', `${window.innerHeight}px`)
  }

  onMount(() => {
    setBodyHeight()
    window.addEventListener('resize', setBodyHeight)
    applyTheme();
    window.matchMedia(DARKMODE).addEventListener('change', applyTheme)
  })

  onDestroy(()=> {
    window.matchMedia(DARKMODE).removeEventListener('change', applyTheme);
  })

  $: console.log(currentTheme)
</script>

<main>
  <Nav toggleTheme={toggleTheme} currentTheme={currentTheme}/>
  <div>
    <h1>Testing Dark Mode</h1>
  </div>
</main>

<style>
  .section {
    height: 100vh;
  }
</style>