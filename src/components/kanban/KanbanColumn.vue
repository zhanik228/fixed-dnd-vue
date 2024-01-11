<template>
  <div class="col">
    <div ref="column" class="kanban-column">
      <h2 class="text-light text-start">{{ title }}</h2>
      <drop-zone />
        <div class="kanban-items" v-for="item in items" :key="item.id">
          <kanban-card :card="item.content" />
        </div>
    </div>
  </div>
</template>

<script>
import KanbanCard from '@/components/kanban/KanbanCard.vue';
import KanbanApi from '@/api/KanbanApi';
import DropZone from './DropZone.vue';

export default {
  data() {
    return {
      items: [],
    };
  },
  components: { KanbanCard, DropZone },
  props: {
    title: {
      required: false,
    },
    id: {
      required: false,
    },
  },
  async mounted() {
    this.$refs.column.dataset.id = this.id;

    setInterval(async () => {
      this.items = await KanbanApi.getItems(this.id);
    }, 1000);
  },
};
</script>
