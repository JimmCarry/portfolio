<template>
  <div class="home">
    <h1>Coding is
      <span class="typed-text">{{ typeValue }}</span>
      <span class="cursor" :class="{'typing': typeStatus}">&nbsp;</span>
    </h1>
    <p>I am trying to be frontend web-developer. Creating and learning about frontend technologies is my pleasure. I´m trying do stuff in clear HTML/CSS and Javascript.
      For more complex projects I am using frameworks like Vuejs and Laravel for some backend work. I am not defend to things like SCSS or tailwind but more work is more experiences. You can look on some my latest projects.
    </p>
  </div>
</template>

<script>
import { reactive, toRefs, onMounted } from 'vue'

export default {
  setup () {

    const state = reactive({
      typeStatus: false,
      typeValue: '',
      typeArray: ['Developer', 'Designer', 'Creator'],
      charIndex: 0,
      typeArrayIndex: 0,
      typingSpeed: 200,
      newTextDelay: 2000,
      erasingSpeed: 100
    })

    const typeText = () => {
      if (state.charIndex < state.typeArray[state.typeArrayIndex].length) {
        if (!state.typeStatus)
          state.typeStatus = true

        state.typeValue += state.typeArray[state.typeArrayIndex].charAt(state.charIndex);
        state.charIndex += 1;

        setTimeout(() => {
          typeText();
        }, state.typingSpeed);

      } else {
        state.typeStatus = false
        setTimeout(() => {
          eraseText();
        }, state.newTextDelay);
      }
    }

    const eraseText = () => {
      if (state.charIndex > 0) {
        if (!state.typeStatus)
          state.typeStatus = true

          state.typeValue = state.typeArray[state.typeArrayIndex].substring(0, state.charIndex - 1);
          state.charIndex -= 1;
          setTimeout(() => {
            eraseText();
          }, state.erasingSpeed);

      } else {
        state.typeStatus = false;
        state.typeArrayIndex += 1;
        if (state.typeArrayIndex >= state.typeArray.length)
          state.typeArrayIndex = 0;

        setTimeout(() => {
          typeText();
        }, state.typingSpeed + 1000);
      }
    }

    onMounted(() => {
      setTimeout(() => {
        typeText()
      }, state.newTextDelay);
    })
    
    return {
      ...toRefs(state),
      typeText
    }
  }
}
</script>

<style lang="scss" scoped>
.home {
  padding: 6rem 0;
  max-width: 600px;
  margin: 0 auto;
}
h1 {
    font-size: 3rem;
    font-weight: normal;

    span.typed-text {
      color: #D2B94B;
    }

    span.cursor {
      display: inline-block;
      margin-left: 3px;
      width: 4px;
      background-color: #fff;
      animation: cursorBlink 1s infinite;
    }

    span.cursor.typing {
      animation: none;
    }
  }

  @keyframes cursorBlink {
    49% { background-color: #fff; }
    50% { background-color: transparent; }
    99% { background-color: transparent; }
  }
</style>

