<template>
  <div
    ref="dropzone"
    class="kanban-dropzone"
    @dragover="handleDragOver"
    @dragleave="handleDragLeave"
    @drop="handleDrop"
  ></div>
</template>

<script>
import KanbanApi from '@/api/KanbanApi';

export default {
  data() {
    return {
      dropZone: null,
    };
  },
  methods: {
    handleDragOver(e) {
      e.preventDefault();
      this.dropZone.classList.add('kanban-dropzone--active');
    },
    handleDragLeave() {
      this.dropZone.classList.remove('kanban-dropzone--active');
    },
    async handleDrop(e) {
      e.preventDefault();
      this.dropZone.classList.remove('kanban-dropzone--active');
      const columnElement = this.dropZone.closest('.kanban-column');
      const columnId = Number(columnElement.dataset.id);
      const dropZonesInColumn = Array.from(
        columnElement.querySelectorAll('.kanban-dropzone'),
      );
      const droppedIndex = dropZonesInColumn.indexOf(this.dropZone);
      const itemId = e.dataTransfer.getData('text/plain');
      const droppedItemElement = document.querySelector(`[data-id="${itemId}"]`);
      // const insertAfter = this.dropZone.parentElement.
      // classList.contains('card-container') ? this.dropZone.parentElement : this.dropZone;

      // insertAfter.after(droppedItemElement);
      // eslint-disable-next-line
      console.log(columnElement, columnId, droppedIndex, droppedItemElement);
      KanbanApi.updateItem(itemId, {
        columnId,
        position: droppedIndex,
      });

      console.log('getItems:', await KanbanApi.getItems(1));
    },
  },
  mounted() {
    this.dropZone = this.$refs.dropzone;
  },
};
</script>
