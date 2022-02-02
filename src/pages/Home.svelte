<script>
  import {onMount} from 'svelte';

  let tattoo_machine = "/img/tattoo_machine.png";
  let instagram_icon = "/img/icons8-instagram.png";
  let tattoos_src = [];
  let src1 = "";
  let src2 = "";

  function randomIntFromInterval(min, max) {
    return Math.floor(Math.random() * (max - min + 1) + min);
  }

  const setRandomImage = (images) => {
    let random1 = randomIntFromInterval(1, 9);
    let random2 = randomIntFromInterval(1, 9);
    if (src1 === random1 && random1 !== 1) {
      random1 = random1 - 1;
    } else {
      random1 = random1 + 1;
    }

    if (src2 === random2 && random2 !== 1) {
      random2 = random2 - 1;
    } else {
      random2 = random2 + 1;
    }
    src1 = "/img/tattoos/pic" + randomIntFromInterval(1, 9) + ".jpg";
    src2 = "/img/tattoos/pic" + randomIntFromInterval(1, 9) + ".jpg";
  };

  const revealImage = (image) => {
    image.classList.remove("hide");
    setTimeout(() => {
      image.classList.add("hide");
    }, 4000);
  };

  for (let i = 1; i < 10; i++) {
    tattoos_src.push("/img/tattoos/pic" + i + ".jpg");
  }

  onMount(() => {
    let images = document.querySelectorAll(".img");
    setInterval(() => {
      setRandomImage(images);
      revealImage(images[randomIntFromInterval(0, 1)]);
    }, 5000);
  });

</script>
<main>
    <div class="container">
    <h1>Marco Di Sotto</h1>
    <p>TATTOO ARTIST</p>
    <img class="tattoo_machine" src={tattoo_machine} alt="A tattoo machine." />

    <span
      class="instagram"
      on:click={() => {
        window.open("https://www.instagram.com/marcopulesh/");
      }}
      style="background-image:url({instagram_icon})"
    />
  </div>
  <div class="wall-background">
    <div class="img hide" style="background-image: url({src1});" />
    <div class="img hide" style="background-image: url({src2});" />
  </div>
</main>

<style lang="scss">
  main {
    text-align: center;
    max-width: 240px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    height: 100vh;
    margin-top: -45px;
  }

  .wall-background {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    overflow: hidden;
    justify-content: space-between;
    align-content: center;
    z-index: 5;
    opacity: .3;
    pointer-events: none;

    .img {
      width: 35em;
      height: 35em;
      background-position: center;
      opacity: 1;
      transition: opacity 0.5s linear;
      box-shadow: 0 0px 53px 67px #fff inset;
      background-repeat: no-repeat;
      background-size: contain;

      @media screen and (max-width: 1123px) {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
      }

      &.hide {
        opacity: 0;
        transition: opacity 0.5s linear;
      }
    }
  }
  .container {
    position: relative;
    z-index: 10;
    text-shadow: 0px 0px 15px white;
  }

  .instagram {
    cursor: pointer;
    display: block;
    width: 48px;
    height: 48px;
    margin: 0 auto;
    z-index: 999999;
    position: relative;
  }

  .tattoo_machine {
    position: absolute;
    top: -210px;
    left: -50px;
    width: 100%;
    height: auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }

    h1 {
      font-size: 4em;
    }

    .tattoo_machine {
      top: -357px;
      left: -180px;
      width: 90%;
    }
  }
</style>