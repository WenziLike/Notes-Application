<template>
  <div>
    <div class="message">
      <p>Messange - {{ message }}</p>
    </div>
  </div>
</template>


<script>
export default {
  props: {
    message: {
      type: String,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
.message {
  text-align: center;
  padding: 2%;
}
p {
  color: #ec0404;
  font-weight: 500;
  font-size: 1.5em;
}
</style>