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
  <section class="content">
    <h1>Aliquam porttitor mauris sit amet orci Aenean</h1>
    <h2>Aliquam porttitor mauris sit amet orci Aenean</h2>
    <h3>Aliquam porttitor mauris sit amet orci Aenean</h3>
    <h3 class="f3">Aliquam porttitor mauris sit amet orci Aenean</h3>
    <p class="p1">Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti.

Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis, mi neque euismod dui, eu pulvinar nunc sapien ornare nisl. Phasellus pede arcu, dapibus eu, fermentum et, dapibus sed, urna.</p>
     <p class="p2">Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel, dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet viverra, tortor libero sodales leo, eget blandit nunc tortor eu nibh. Nullam mollis. Ut justo. Suspendisse potenti. Sed egestas, ante et vulputate volutpat, eros pede semper est, vitae luctus metus libero eu augue. Morbi purus libero, faucibus adipiscing, commodo quis, gravida id, est. Sed lectus. Praesent elementum hendrerit tortor. Sed semper lorem at felis. Vestibulum volutpat, lacus a ultrices sagittis</p>
  </section>
</main>

<style>
  .section {
    height: 100vh;
  }
</style>