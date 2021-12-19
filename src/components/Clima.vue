<template>
  <div class="clima">
    <img src="" alt="" />
  </div>
</template>

<script>
export default {
  name: "Clima",
  props: {
    cidade: {
      type: String,
      default: "Brasilia",
    },
  },
  methods: {
    buscarClima() {
      fetch("")
        .then((r) => r.json())
        .then((r) => {
          return r;
        });
    },
  },
  created: {},
};
</script>

<style>
.clima {
  position: absolute;
  max-width: 900px;
  border: 2px solid #000;
  border-radius: 6px;
  background: #fff;
}
</style>
