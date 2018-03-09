<template lang="html">
    <div class="" id="app">
        <app-header></app-header>
        <app-league></app-league>
        <app-footer></app-footer>
<!-- <div>Icons made by <a href="http://www.freepik.com" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div> -->
    </div>
</template>

<script>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import League from './components/league/League.vue'

export default {
    components: {
        appHeader: Header,
        appFooter: Footer,
        appLeague: League
    }
}
</script>

<style lang="scss">
* {
    font-family: 'Exo 2', 'Roboto', sans-serif;
    color: #fafafa;
    box-sizing: border-box;
}

body {
    background-color: #323232;
}

h1 {
    font-family: 'Audiowide', cursive;
    text-transform: uppercase;
    letter-spacing: 3px;
    margin: 0;
    font-size: 40px;

    img {
        max-width: 40px;
    }
}

h3 {
    font-family: 'Audiowide', cursive;
    font-size: 30px;
    text-align: center;
}

h4 {
    width: 100%;
    text-align: center;
    margin-bottom: 15px;
}

table {
    width: 100%;
    border-bottom: 0 solid #777;
    border-collapse: collapse;
    background-color: #555;
    border-radius: 5px;

    tr {
        border-bottom: 1px solid #777;
        border-collapse: collapse;

        td, th {
            text-align: center;
            border-bottom: 1px solid #777;
            border-collapse: collapse;
            padding: 10px 0;
        }
    }

    tr:last-of-type,
    tr:last-of-type td {
        border-bottom: none !important;
    }
}

a:link,
a:visited {
    color: #fafafa;
    text-decoration: none;
}
a:hover,
a:active,
a:focus {
    color: #f00;
    text-decoration: none;
}

img {
    width: 100%;
}

.material-icons {
  font-family: 'Material Icons';
  font-weight: normal;
  font-style: normal;
  font-size: 24px;  /* Preferred icon size */
  display: inline-block;
  line-height: 1;
  text-transform: none;
  letter-spacing: normal;
  word-wrap: normal;
  white-space: nowrap;
  direction: ltr;

  /* Support for all WebKit browsers. */
  -webkit-font-smoothing: antialiased;
  /* Support for Safari and Chrome. */
  text-rendering: optimizeLegibility;

  /* Support for Firefox. */
  -moz-osx-font-smoothing: grayscale;

  /* Support for IE. */
  font-feature-settings: 'liga';
}
</style>
