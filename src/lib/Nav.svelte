<script lang="ts">
  import pacmanLogo from '../assets/logo.svg'
  export let toggleTheme
  export let currentTheme

  console.log(currentTheme)

</script>

<nav class="nav">
  <div class="nav-icon">
    <div class="icon-inner"></div>
    <img src={pacmanLogo} class="pacman" alt="Invoice Logo"/>
  </div>
  <div class="nav-buttons">
    <div class="darkmode">
      {#if currentTheme === 'light'}
        <img on:click={toggleTheme} class="darkmode_icon" src="/src/assets/icon-moon.svg" alt="Toggle Dark Mode"/>
      {:else}
        <img on:click={toggleTheme} class="darkmode_icon" src="/src/assets/icon-sun.svg" alt="Toggle Dark Mode"/>
      {/if}
    </div>
    <div class="user">
      <div class="avatar-container">
        <img class="avatar" src="src/assets/image-avatar.jpg" alt="Avatar"/>
      </div>
    </div>
  </div>
</nav>

<style>

  .nav {
    display: flex;
    flex-direction: row;
    width: 100vw;
    height: 5em;
    background-color: #1E2139;
    position: sticky;
    top: 0px;
  }

  .nav-icon {
    display: flex;
    position: relative;
    align-items: center;
    justify-content: center;
    width: 5.5em;
    height: 100%;
    border-top-right-radius: 30px;
    border-bottom-right-radius: 30px;
    background-color: #7C5DFA;
  }

  .icon-inner {
    width: 100%;
    height: 50%;
    margin-top: auto;
    background-color: #9277FF;
    border-top-left-radius: 25px;
    border-bottom-right-radius: inherit;
  }

  .pacman {
    position: absolute;
    width: 40%;
  }

  .nav-buttons {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: row;
    margin-left: auto;
    height: 100%;
  }

  .darkmode {
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    height: 100%;
    width: 5em;
  }

  .darkmode_icon {
    width: 30%;
    height: 30%;
    cursor: pointer;
  }

  .user {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 6em;
    height: 100%;
    border-left: 1px solid #888eb06d;
  }

  .avatar-container {
    position: relative;
    width: 40%;
    overflow: hidden;
    border-radius: 50%;
  }

  .avatar-container::before {
    content: "";
    display: block;
    padding-top: 100%;

  }

  .avatar {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    width: 100%;
    height: 100%;
  }

</style>