<template>
    <div class="typeHolder">
        <div class="texttype"></div>
    </div>
</template>

<script>
import Typed from 'typed.js'

var options = {
  strings: ['Front End Development', 'UX &amp; Usability Design', 'Photography', 'Cycling', 'Nonsense'],
  typeSpeed: 50,
  loop: true,
  backSpeed: 35,
  backDelay: 3500
}

export default {
  mounted: function () {
    var typed = new Typed('.texttype', options)
  }
}
</script>

<style lang="less">
    .typeHolder {
        display: block;
        font-size: 40px;
        font-size: 4vw;
        line-height: 1;
        margin: 0 0 .5em;
        color: #fff;
        font-weight: 200;
        .texttype {
            display: inline;
        }
        .typed-cursor {
            opacity: 1;
            -webkit-animation: typedjsBlink .7s infinite;
            animation: typedjsBlink .7s infinite;
            animation-iteration-count: infinite;
            color: rgba(0,0,0,0);
            border-bottom: 3px solid #fff;
            font-size: 1em;
            width: .5em;
            display: inline-block;
            position: relative;
            bottom: 5px;
            margin-left: .1em;
        }
    }

    @keyframes typedjsBlink{
        0% { opacity: 1; }
        50% { opacity: 0.0; }
        100% { opacity: 1; }
    }

    @media screen and (max-width: 40em) {
        .typeHolder {
            font-size: 30px;
            font-size: 6.5vw;
        }
    }
</style>
