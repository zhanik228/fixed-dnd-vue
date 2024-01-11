<template>
  <div class="card-container" ref="thisCard">
    <drop-zone />
  <div
    class="card w-full"
    draggable
    @dragstart="handleDragStart"
  >
    <img :src="card.picture.large"
         class="card-img-top" alt="Chicago Skyscrapers"/>
    <div class="card-body">
      <h5 class="card-title">
        <router-link :to="`profile/${card.email}`">
          {{ card.name.title }} {{ card.name.first }} {{ card.name.last }}
        </router-link>
      </h5>
      <p class="card-text">
        {{ card.location.country }}, {{ card.location.city }}
      </p>
    </div>
    <ul class="list-group list-group-light list-group-small">
      <li class="list-group-item px-4">Number: {{ card.phone }}</li>
      <li class="list-group-item px-4">Dapibus ac facilisis in</li>
      <li class="list-group-item px-4">Vestibulum at eros</li>
    </ul>
  </div>
  <drop-zone />
  </div>
</template>

<script>
import DropZone from './DropZone.vue';

export default {
  components: {
    DropZone,
  },
  props: {
    card: {
      required: false,
    },
  },
  methods: {
    handleDragStart(event) {
      event.dataTransfer.setData('text/plain', this.card.email);
    },
  },
  mounted() {
    this.$refs.thisCard.dataset.id = this.card.email;
  },
};
</script>

<style scoped>
.card {
  z-index: 2;
}
</style>
