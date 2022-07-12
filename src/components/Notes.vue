<template>
  <div class="notes">
    <div class="container">
      <div class="notes__top">
        <h2 class="notes__title">
          {{ notes.length > 0 ? words.infobar[lang] : words.noinfobar[lang] }}
        </h2>
        <button class="notes__btn" @click="grid = !grid">
          <img src="@/assets/img/list.png" alt="" v-if="grid" />
          <img src="@/assets/img/grid.png" alt="" v-else />
          <span>{{ grid ? words.list[lang] : words.grid[lang] }}</span>
        </button>
      </div>
      <div class="notes__list" :class="{ grid: !grid }">
        <NoteItem
          :lang="lang"
          :grid="grid"
          v-for="note in notes"
          :key="note.id"
          :note="note"
          @delNote="$emit('delNote', note.id)"
          @changeNote="$emit('changeNote', note.id)"
        />
      </div>
    </div>
  </div>
</template>

<script>
import NoteItem from "@/components/NoteItem.vue";

export default {
  components: {
    NoteItem,
  },
  data() {
    return {
      grid: true,
    };
  },
  inject: ['words'],
  props: {
    lang: String,
    notes: {
      typeof: Array,
      default: [],
    },
  },
};
</script>

<style>
.notes {
  margin-top: 50px;
}

.notes__list {
  margin-top: 50px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 200px;
  gap: 25px;
}
.notes__list.grid {
  grid-template-columns: 1fr;
}
.notes__top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.notes__title {
  font-size: 22px;
  line-height: 28px;
  color: #323232;
}
.notes__btn {
  outline: none;
  border: none;
  width: 120px;
  height: 56px;
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.11),
      rgba(103, 80, 164, 0.11)
    ),
    #fffbfe;
  box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15),
    0px 1px 3px rgba(0, 0, 0, 0.3);
  border-radius: 16px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 15px;
}
.notes__btn span {
  font-size: 14px;
  line-height: 20px;
  color: #6750a4;
  font-family: "RM";
}
</style>