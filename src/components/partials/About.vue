<template>
  <div class="about">
    <bubbleOne></bubbleOne>
    <div class="about-text">
      <h2><span>Where to?</span></h2>
      <p v-html="texts[activeState]"></p>
    </div>
    <bubbleTwo></bubbleTwo>
  </div>
</template>

<script>
import bubbleOne from '../animations/BubbleOne.vue';
import bubbleTwo from '../animations/BubbleTwo.vue';

export default {
  name: 'about',
  components: {
    bubbleOne,
    bubbleTwo
  },
  data () {
    return {
      activeState: 'start',
      // TODO: move to json?
      texts: {
        start: 'This project is a collaboration between three students from Digital Design and Web Development at Yrgo. We wanted to explore how a website could be brought to life by adding decorative animations to it. We have experimented with three different triggers - scroll, hover and click. This landing page is quite boring and grey, have a look around to see the difference some animations and colour can make to it!',
        scroll: 'Scroll animations can be added to liven up a lengthy page through triggering different animations when scrolling. A popular scrolling effect is parallax, where an element can pop in from different directions. Applying scroll animations can give your page a dramatic effect or a touch of elegance. Scroll down to see some animations that we’ve experimented with and see if you like them!',
        hover: 'The best hover effects can enhance the user’s overall experience of a website. They draw attention to important information and engage the user. Hover effects are often used in designs to improve style and usability, whilst adding an extra energy to the page. On this page we have experimented with different hover animations. Hover around and see how it affects your own experience!',
        click: 'On this webpage we have experimented with click-triggered animations. Click animation is often used for buttons and menus, but it can also be used with decorative animations that create user interaction. Click animations can incorporate drag elements, drawing, double click and hold-in click, and are a fun way to enhance user engagement. Have a click around!'
      }
    }
  },
  created () {
    Event.$on('activeState', clickedNavItem => {
      this.activeState = clickedNavItem;
    });
  }
}
</script>

<style lang="scss">
.about {
  align-items: center;
  display: flex;
  height: 650px;
  padding: 0 5em 0 0;
  position: relative;
  .about-text {
    display: flex;
    flex-direction: row;
    justify-content: center;
    width: 100%;
    p {
      width: 500px;
    }
    h2 {
      transform: rotate(-90deg) translate(70px, 30px);
      span {
        border-color: #000;
      }
    }
  }
}
@media screen and (max-width: 1440px) {
  .about {
    height: 750px;

  }
}
@media screen and (max-width: 1000px) {
  .about {
    height: 870px;
    padding: 0 2em 0 0;
    .about-text {
      justify-content: flex-start;
    }
    p {
      width: 100%;
    }
  }
}
@media screen and (max-width: 820px) {
  .about {
    height: 750px;
  }
}
@media screen and (max-width: 750px) {
  .about {
    height: 800px;
    padding: 0 3em;
    .about-text {
      align-items: center;
      flex-direction: column;
      h2 {
        transform: rotate(0) translate(0, 0);
        width: 500px;
      }
    }
  }
}
@media screen and (max-width: 690px) {
  .about {
    height: 580px;
    .about-text {
      h2, p {
        width: 100%;
      }
    }
  }
}
@media screen and (max-width: 480px) {
  .about {
    align-items: flex-start;
    height: 480px;
  }
}
@media screen and (max-width: 430px) {
  .about {
    padding: 0 1em;
  }
}
@media screen and (max-width: 320px) {
  .about {
    height: 460px;
  }
}
</style>
