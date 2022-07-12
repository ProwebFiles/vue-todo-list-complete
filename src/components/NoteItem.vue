<template>
  <div class="notes__item">
    <div class="notes__item-top" :class="{ between: !grid }">
      <h3 class="notes__item-title">{{ note.title }}</h3>
      <p class="notes__item-date">{{ note.date }}</p>
    </div>
    <p class="notes__item-descr">{{ note.descr }}</p>
    <div class="notes__item-btns">
      <button
        class="notes__item-btn change"
        @click="$emit('changeNote', note.id)"
      >
        <img src="@/assets/img/change.png" alt="" />
        <span>{{ words.editbtn[lang] }}</span>
      </button>
      <button class="notes__item-btn delete" @click="$emit('delNote', note.id)">
        <img src="@/assets/img/delete.png" alt="" />
        <span>{{ words.deledit[lang] }}</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  inject: ['words'],
  props: {
    lang: String,
    grid: {
      typeof: Boolean,
      default: true,
    },
    note: {
      typeof: Object,
      default: {
        title: "",
        descr: "",
        date: "",
        id: 0,
      },
    },
  },
};
</script>

<style>
.notes__item {
  background: linear-gradient(
      0deg,
      rgba(103, 80, 164, 0.05),
      rgba(103, 80, 164, 0.05)
    ),
    #fffbfe;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.3),
    0px 1px 3px 1px rgba(0, 0, 0, 0.15);
  border-radius: 16px;
  padding: 16px 16px 28px 16px;
}

.notes__item-title {
  font-size: 16px;
  line-height: 24px;
  color: #1c1b1f;
  font-family: "RM";
}
.notes__item-date {
  font-size: 14px;
  line-height: 20px;
  color: #cac4d0;
}
.notes__item-descr {
  font-size: 14px;
  line-height: 20px;
  color: #49454f;
  margin-top: 16px;
  margin-bottom: 30px;
}

.notes__item-btns {
  display: flex;
  justify-content: flex-end;
  gap: 10px;
}
.notes__item-btn {
  display: flex;
  align-items: center;
  gap: 10px;
  background: transparent;
  padding: 12px;
  border-radius: 5px;
}
.notes__item-btn span {
  font-size: 14px;
  line-height: 20px;
  font-family: "RM";
  text-transform: uppercase;
}
.change {
  color: #6750a4;
  transition: background 300ms;
}

.change:hover {
  background: #e6ddff;
}
.delete {
  color: #cf1b1b;
  transition: background 300ms;
}
.delete:hover {
  background: #ffe1e1;
}
.between {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
</style>