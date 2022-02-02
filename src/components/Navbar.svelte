<script>
  import { onMount } from "svelte";

  let showMobileMenu = false;
  let logo = "/img/tattoo.png";

  const navItems = [
    { label: "ABOUT ME", href: "about" },
    { label: "GET IN TOUCH", href: "contacts" },
  ];

  const handleMobileIconClick = () => {
    const mediaListener = window.matchMedia("(max-width: 767px)");

    if (!mediaListener.matches) {
      return
    }

    return (showMobileMenu = !showMobileMenu);
  };

  const mediaQueryHandler = (e) => {
    if (!e.matches) {
      showMobileMenu = false;
    }
  };

  onMount(() => {
    const mediaListener = window.matchMedia("(max-width: 767px)");

    mediaListener.addListener(mediaQueryHandler);
  });
</script>

<nav>
  <div class="inner">
    <a href="/"><span class="logo" style="background-image:url({logo})" /></a>
    <div
      on:click={handleMobileIconClick}
      class={`mobile-icon${showMobileMenu ? " active" : ""}`}
    >
      <div class="middle-line" />
    </div>
    <ul class={`navbar-list${showMobileMenu ? " mobile" : ""}`}>
      <li on:click={handleMobileIconClick} class="home">
        <a href="/">HOME</a>
      </li>
      {#each navItems as item}
        <li on:click={handleMobileIconClick}>
          <a href={item.href}>{item.label}</a>
        </li>
      {/each}
    </ul>
  </div>
</nav>

<style lang="scss">
  .logo {
    width: 3em;
    height: 3em;
    background-position: center;
    background-size: contain;
    justify-self: start;
    display: none;
    background-size: 80%;
    background-repeat: no-repeat;
    position: relative;
    cursor: pointer;

    &:after {
      content: "MDS";
      position: absolute;
      right: -35px;
      top: 25%;
      color: #ff3e00;
    }
  }

  .home {
    display: block;
  }
  nav {
    background-color: white;
    height: 45px;
    z-index: 15;
    color: #ff3e00;
  }

  .inner {
    padding-left: 20px;
    padding-right: 20px;
    margin: auto;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    height: 100%;
  }

  .mobile-icon {
    width: 25px;
    height: 14px;
    position: relative;
    cursor: pointer;
  }

  .mobile-icon:after,
  .mobile-icon:before,
  .middle-line {
    content: "";
    position: absolute;
    width: 100%;
    height: 2px;
    background-color: #ff3e00;
    transition: all 0.4s;
    transform-origin: center;
  }

  .mobile-icon:before,
  .middle-line {
    top: 0;
  }

  .mobile-icon:after,
  .middle-line {
    bottom: 0;
  }

  .mobile-icon:before {
    width: 66%;
  }

  .mobile-icon:after {
    width: 33%;
  }

  .middle-line {
    margin: auto;
  }

  .mobile-icon:hover:before,
  .mobile-icon:hover:after,
  .mobile-icon.active:before,
  .mobile-icon.active:after,
  .mobile-icon.active .middle-line {
    width: 100%;
  }

  .mobile-icon.active:before,
  .mobile-icon.active:after {
    top: 50%;
    transform: rotate(-45deg);
  }

  .mobile-icon.active .middle-line {
    transform: rotate(45deg);
  }

  .navbar-list {
    display: none;
    width: 100%;
    justify-content: center;
    margin: 0;
    padding: 0 40px;
    z-index: 15;
  }

  .navbar-list.mobile {
    background-color: white;
    position: fixed;
    display: block;
    height: calc(100% - 45px);
    bottom: 0;
    left: 0;
    z-index: 15;
    color: #ff3e00;
  }

  .navbar-list li {
    list-style-type: none;
    position: relative;
  }

  .navbar-list a {
    color: #ff3e00;
    text-decoration: none;
    display: flex;
    height: 45px;
    align-items: center;
    padding: 0 10px;
    font-size: 13px;
  }

  @media only screen and (min-width: 767px) {
    .mobile-icon {
      display: none;
    }

    .logo {
      display: block;
    }

    .home {
      display: none;
    }

    .navbar-list {
      display: flex;
      padding: 0;
    }

    .navbar-list a {
      display: inline-flex;
    }
  }
</style>
