<template>
  <div class="box" :class="{open: messageText, close: !messageText}">
    <div class="header">
      <a @click="closeMessage" class="close">&times;</a>
    </div>
    <div class="mess">
      <p class="text text-center" name="message">{{messageText}}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      messageText: null,
    }
  },
  methods: {
    closeMessage() {
      this.$store.dispatch("closeMessage");
    },
  },
  computed: {
    message() {
      return this.$store.getters.message;
    },
  },
  watch: {
    message(val) {
      this.messageText = val;
      setTimeout(() => this.$store.dispatch("closeMessage"), 5000);
    }
  }
};
</script>

<style scoped lang="scss">
.box {
  z-index: 4000;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  @media (max-width: 600px) {
    width: 100%;
  }
  background: linear-gradient(#43cea2, #185a9d);
  box-shadow: 2px 2px 12px 2px #444;
  transition: .5s all ease-in-out;
  transform: translateY(-100vh);
  &.open {
    transform: translateY(0);
  }
  .header {
    strong, a {
      color: #fff;
    }
  }
  .mess {
    padding-top: 12px;
    p {
      color: rgb(250, 242, 242);
      font-size: 1rem;
      @media (max-width: 600px) {
        font-size: .5rem;
      }
    }
  }
}

</style>
