<template>
  <span @click.stop>
    <b-badge @click="enabled = true" class="mt-2" href="#" variant="info" pill>Edit</b-badge>
    <div :class="type == 'item'? 'item-fix': '' " id="form" v-if="enabled">
      <b-form-input
        autofocus
        @focusout="enabled = false"
        class="mr-1"
        v-model="content"
        size="sm"
        :placeholder="label"
      ></b-form-input>
      <b-button @mousedown.prevent @click="changeTitle" variant="info" size="sm">✔</b-button>
    </div>
  </span>
</template>

<script>
export default {
  props: {
    label: {
      type: String
    },
    type: {
      type: String
    }
  },
  methods: {
    changeTitle() {
      if (this.content.length < 1) return;
      this.$emit("changeItem", this.content);
      this.content = "";
      this.enabled = false;
    }
  },
  data() {
    return {
      enabled: false,
      content: ""
    };
  }
};
</script>

<style scoped>
#form {
  width: 150px;
  background-color: rgb(240, 240, 240);
  position: absolute;
  z-index: 2;
  border-radius: 5px;
  padding: 5px;
  display: flex;
}
.item-fix {
  left: 50%;
}
@media (max-width: 576px) {
  .item-fix {
    left: 70%;
  }
}
@media (max-width: 480px) {
  .item-fix {
    left: 50%;
  }
}
</style>