<script>
  import { link } from "svelte-spa-router";
  import LogoGrablee from "~/shared/icons/logograblee.svg";

  import SuperSearch from "~/widgets/super-search/index.svelte";
  import ThemeButtom from "~/widgets/theme-button/index.svelte";
  import BlurLayout from "~/features/blur-layout.svelte";
  import WallLayout from "~/features/wall-layout.svelte";

  let themeDark = false;
  let changeTheme = (e) => {
    themeDark = !themeDark;
  };
  let elapsedSearch = true;

  let allowClick = false;
  let onDbClick = (fn) => (e) => {
    if (allowClick) {
      fn(e);
      return;
    }
    allowClick = true;
    setTimeout(() => {
      allowClick = false;
    }, 200);
  };
</script>

<main class="greeting-page">
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  <div
    class={`greeting-page__fixed-item greeting-page__fixed-item${
      themeDark && "-dark"
    }`}
    on:click={onDbClick(changeTheme)}
  >
    <BlurLayout>
      <div class="description-block">
        <div class="description-block__header">
          <div class="absolute-block">
            <ThemeButtom bind:dark={themeDark} hide={!elapsedSearch} />
          </div>
          <div class="absolute-block">
            <SuperSearch bind:elapsed={elapsedSearch} />
          </div>
        </div>
        <div class="description-block__content">
          <div class="prologue-block">
            <div class="prologue-block__heading">
              <img class="logo" src={LogoGrablee} alt="logo white" />
            </div>
            <div class="prologue-block__item">
              <div class="spantext-block">
                <span class="spantext-block__text">
                  Our app is a quick way to share information about yourself or
                  learn more about the person you just met!
                </span>
              </div>
            </div>
            <div class="prologue-block__toggle">
              <button class="arrow-button">
                <div class="arrow-button__content">
                  <h1 class="medium-title">SEARCH</h1>
                </div>
              </button>
              <a href="/sandbox" use:link>
                <button class="arrow-button">
                  <div class="arrow-button__content">
                    <h1 class="medium-title">SHARE</h1>
                  </div>
                </button>
              </a>
            </div>
          </div>
        </div>
        <div class="description-block__footer">
          <h3 class="footer-description">about project</h3>
        </div>
      </div>
    </BlurLayout>
  </div>
  <!--
  <div class="greeting-page__floated-item">
    <WallLayout>
      <div class="wall-content" />
    </WallLayout>
  </div>
-->
</main>

<style lang="scss">
  .greeting-page {
    width: 100%;
    min-height: 720px;
    height: 100vh;
    position: relative;

    &__fixed-item {
      position: fixed;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      width: 100%;
      overflow: hidden;

      transition: background-color 0.5s;
      background-color: rgb(250, 250, 250);

      &-dark {
        background-color: rgb(0, 0, 0);
      }
    }

    &__floated-item {
      position: absolute;
      top: 100%;
      left: 0;
      width: 100%;
      height: 1200px;
      overflow: hidden;
    }
  }

  .footer-description {
    font-size: 21px;
    font-family: Comfortaa;
    text-align: center;
    margin: 0;
    color: #98329f;
    line-height: 60px;
  }

  .absolute-block {
    position: absolute;
    top: 0;
    left: 0;
    padding: 10px;
    width: 100%;
    height: 100%;
  }

  .description-block {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    height: 100%;
    position: relative;
    top: 0;
    left: 0;
    &__header {
      width: 100%;
      max-width: 720px;
      height: 80px;
      min-height: 80px;
      padding: 10px;
      position: relative;
    }
    &__content {
      width: 100%;
      max-width: 360px;
      min-height: 360px;
      padding: 20px;
    }
    &__footer {
      max-width: 720px;
      width: 100%;
      height: 80px;
      padding: 10px;
    }
  }

  .prologue-block {
    width: 100%;
    height: 100%;
    color: #f9f9f9;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-direction: column;
    gap: 40px;
    &__heading {
      width: 100%;
      height: 70px;
    }
    &__item {
      width: 100%;
      min-height: 120px;
    }
    &__toggle {
      width: 100%;
      height: 70px;
      padding: 0 10px;
      display: flex;
      flex-direction: column;
      gap: 20px;
    }
  }

  .medium-title {
    margin: 0;
    padding: 0;
    font-size: 32px;
    text-align: center;
    line-height: 48px;
    color: white;
    font-family: Comfortaa;
  }

  .spantext-block {
    text-align: center;
    &__text {
      font-family: Comfortaa;
      font-size: 21px;
      line-height: 28px;
      text-align: center;
    }
    &__p {
      padding: 10px;
      font-size: 21px;
      border: 2px solid #f9f9f9;
      border-radius: 15px;
    }
  }

  .arrow-button {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    gap: 10px;
    top: 0;
    left: 0;
    padding: 20px;
    border: 2px solid #f9f9f9;
    border-radius: 40px;
    padding: 0 10%;
    background: none;
    &__content {
      height: 48px;
    }
    &__arrow {
      position: absolute;
      right: calc(10% - 10px);
      width: 42px;
      height: 100%;
      transition: transform 0.5s;
      transform: translate(0, 0);
      display: flex;
      justify-content: center;
    }

    &:hover {
      .arrow-button__arrow {
        transform: translate(10px, 0);
      }
    }
  }

  .arrow-img {
    display: block;
    width: 100%;
    filter: invert(1);
  }

  .wall-content {
    width: 100%;
    height: 100%;
    background-color: #f9f9f9;
    border-radius: 30px;
  }

  .logo {
    width: 100%;
    display: block;
    margin: auto;
  }

  @keyframes auto-change-theme {
    0% {
      background-color: rgb(255, 255, 255);
    }
    49% {
      background-color: rgb(255, 255, 255);
    }
    50% {
      background-color: rgb(0, 0, 0);
    }
    99% {
      background-color: rgb(0, 0, 0);
    }
    100% {
      background-color: rgb(255, 255, 255);
    }
  }
</style>
