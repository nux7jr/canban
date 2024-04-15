<template>
  <div class="filter">
    <v-tooltip location="top" text="Сортировка по возрастанию рейтинга">
      <template v-slot:activator="{ props }">
        <v-btn v-bind="props" icon="mdi-sort-ascending" density="compact" variant="tonal" color="blue"
          :disabled="!cards.length" @click="filterByRating" />
      </template>
    </v-tooltip>
    <v-tooltip location="top" text="Сортировка по убыванию рейтинга">
      <template v-slot:activator="{ props }">
        <v-btn v-bind="props" icon="mdi-sort-descending" density="compact" variant="tonal" color="blue"
          :disabled="!cards.length" @click="filterByDescending" />
      </template>
    </v-tooltip>
    <v-tooltip location="top" text="Без сортировки">
      <template v-slot:activator="{ props }">
        <v-btn v-bind="props" icon="mdi-sort-variant-remove" density="compact" variant="tonal" color="red"
          :disabled="!cards.length" @click="filterByNoSort" />
      </template>
    </v-tooltip>
  </div>
</template>
<script setup>

const props = defineProps(['cards'])
const emit = defineEmits(['update:cards'])

function filterByRating() {
  const sortedCards = props.cards.sort((a, b) => b.rating.rate - a.rating.rate);
  emit('update:cards', sortedCards);
}

function filterByDescending() {
  const sortedCards = props.cards.sort((a, b) => a.rating.rate - b.rating.rate);
  emit('update:cards', sortedCards);
}

function filterByNoSort() {
  const originalOrder = props.cards.sort((a, b) => a.id - b.id);
  emit('update:cards', originalOrder);
}
</script>
<style lang="scss" scoped>
.filter {
  background-color: white;
  border-radius: 10px;
  padding: 15px;

  display: flex;
  justify-content: flex-end;
  gap: 10px;
  margin-bottom: 20px;
}
</style>