<template>
  <div v-on:mouseover="hoverAnimate" v-on:mouseleave="hoverOut" class="ux-text">
    <h2><span>What not to!</span></h2>
    <p v-html="texts[activeState]"></p>
  </div>
</template>

<script>
export default {
  name: 'uxText',
  data () {
    return {
      activeState: 'start',
      // TODO: move to json?
      texts: {
        start: 'This is a page with decorative animations. We want to inspire you to use them, but doing so sparingly. This matters to the website’s performance as well as keeping the user focused on the most important content. Animations can bring life to a website but it can also disorientate the user if there is too much happening on the page at the same time. It’s important to find a good balance. To get the best experience, visit this webpage in a Chrome browser.',
        scroll: 'Scroll animations are popular because they can be used on all devices. If you’re using fly-in animations when scrolling, try to use them sparingly so they don’t overwhelm the user. It’s also important to show the user that they can scroll down. You can use either a scroll icon or let some content from the next section become visible at the section above it. Use scroll-triggered animations for secondary content to minimise the risk of wearing down the user’s patience.',
        hover: 'When working with a full-screen hover animation, the trick is to impress users without overwhelming them. The design should remain simple – a clean background with an easy to read sans serif typeface. Hover effects don’t work on touch devices or mobile phones, so here you have to activate the effect by utilising actions such as shaking, swiping, or slanting. On this page, the hover section will not be visible when looking at a phone.',
        click: 'You have to show where the user should click and interact with an element, if not, they may miss it. To indicate that the user is supposed to click on an animation, you can change the mouse to a different icon when hovering over the object. Click animations will work on mobile devices aswell, but remember to avoid placing any click elements at the bottom of the screen where users usually swipe to get to the next section.'
      },
      scrolling: false
    }
  },
  methods: {
    scrollAnimate() {
      const uxText = this.$el;
      window.clearTimeout( this.scrolling );
      uxText.classList.add('skew-text');
      this.scrolling = setTimeout(function() {
        uxText.classList.remove('skew-text');
      }, 66);
    },
    hoverAnimate() {
      Event.$emit('uxTextHover');
    },
    hoverOut() {
      Event.$emit('uxTextOut');
    }
  },
  created () {
    Event.$on('activeState', clickedNavItem => {
      this.activeState = clickedNavItem;
    });
    Event.$on('rollActive', () => {
      this.$el.classList.add('skew-text-click');
    });
    Event.$on('rollDone', () => {
      this.$el.classList.remove('skew-text-click');
    });
    Event.$on('rollHoverActive', () => {
      this.$el.classList.add('skew-text');
    });
    Event.$on('rollHoverDone', () => {
      this.$el.classList.remove('skew-text');
    });
    Event.$on('scrolling', () => {
      this.scrollAnimate();
    });
  }
}

</script>

<style lang="scss">
.ux-text {
  align-items: flex-start;
  color: #fff;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
  position: absolute;
  right: 200px;
  top: 250px;
  transition: all 0.5s linear;
  h2 {
    transform: rotate(-90deg) translate(12px, -30px);
    transition: all 0.5s linear;
  }
  p {
    width: 500px;
  }
}
.click .ux-text {
  cursor: pointer;
}

@keyframes blur {
  0%, 100% {
    transform-origin: center center;
    transform: skew(0) translate(0,0);
  }
  50% {
    transform-origin: center center;
    transform:  skew(-5deg) translate(5px, 10px);
  }
}
.skew-text-click {
  animation: 2s ease-in-out infinite reverse blur;
  h2 {
    text-decoration: line-through;
  }
}
.skew-text {
  transform-origin: center center;
  transform: skew(-5deg) translate(5px, 10px);
  h2 {
    text-decoration: line-through;
  }
}

@media screen and (max-width: 1350px) {
  .ux-text {
    right: 150px;
    top: 170px;
  }
}
@media screen and (max-width: 1150px) {
  .ux-text {
    top: 250px;
  }
}
@media screen and (max-width: 1000px) {
  .ux-text {
    top: 200px;
  }
}
@media screen and (max-width: 850px) {
  .ux-text {
    right: 120px
  }
}
@media screen and (max-width: 750px) {
  .ux-text {
    align-items: center;
    flex-direction: column;
    justify-content: flex-start;
    right: 0;
    top: 170px;
    width: calc(100vw - 60px);
    h2 {
      transform: rotate(0) translate(0, 0);
      width: 500px;
    }
  }
}
@media screen and (max-width: 690px) {
  .ux-text {
    padding: 0 3em 0;
    h2, p {
      width: 100%;
    }
  }
}
@media screen and (max-width: 600px) {
  .ux-text {
    width: calc(100vw - 40px);
  }
}
@media screen and (max-width: 430px) {
  .ux-text {
    padding: 0 1em 0;
  }
}
</style>
