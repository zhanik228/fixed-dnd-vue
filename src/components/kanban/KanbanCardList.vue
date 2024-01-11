<template>
  <div v-if="items">
    <div ref="item" class="kanban-items" v-for="item in items" :key="item.id">
    <kanban-card :card="item.content" />
  </div>
  </div>
</template>

<script>
import DropZone from '@/view/DropZone';
import KanbanCard from './KanbanCard.vue';

export default {
  components: {
    KanbanCard,
  },
  props: {
    items: {
      required: false,
    },
  },
  mounted() {
    const topDropzone = DropZone.createDropZone();
    this.$refs.item.prepend(topDropzone);
    const bottomDropzone = DropZone.createDropZone();
    this.$refs.item.appendChild(bottomDropzone);
  },
};
</script>
