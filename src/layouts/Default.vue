<template>
  <div class="layout">
    <div class="header pa3 bg-yellow">
      <div class="mw9 center">
        <g-link
          to="/"
        >
          patterns
        </g-link>
      </div>
    </div>
    <slot />
  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<style>
@font-face {
  font-family: pilowlava;
  src: url('../../fonts/pilowlava-master/Fonts/webfonts/Pilowlava-Regular.woff');
  font-weight: normal;
}

.header {
  font-family: pilowlava;
}

.header a {
  text-decoration: none;
  color: #00449E;
  font-size: 2em;
}
</style>
