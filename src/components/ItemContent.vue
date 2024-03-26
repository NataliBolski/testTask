<template>
  <div class="content">
    <span class="header"> {{ item.name }}</span>

    <div class="detail" v-for="attr in innerItem.attributes" :key="attr.code">
      <div class="field">
        <span class="title">code:</span>
        <input :value="attr.code" />
      </div>

      <div class="field">
        <span class="title">name:</span>
        <input :value="attr.name" />
      </div>

      <div v-if="'color' in attr" class="field">
        <span class="title">color:</span>
        <input :value="attr.color" />
      </div>

      <div v-if="'size' in attr" class="field">
        <span class="title">size:</span>
        <span>
          <input :value="attr.size.width" type="number" /> x
          <input :value="attr.size.height" type="number" />
        </span>
      </div>

      <div v-if="'weight' in attr" class="field">
        <span class="title">weight:</span>
        <input :value="attr.weight" type="number" />
      </div>
    </div>
    <div class="add">
      <label>
        type
        <select ref="selectRef">
          <option value="color">color</option>
          <option value="size">size</option>
          <option value="weight">weight</option>
        </select>
      </label>

      <button @click="addItem">Add</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits, ref, computed } from "vue";
import { Product } from "./types";

const props = defineProps<{
  item: {
    id: number;
    name: string;
    attributes: Product["attributes"];
  };
}>();

const emit = defineEmits(["add"]);

const selectRef = ref<HTMLSelectElement>();
const innerItem = computed(() => props.item);

const addItem = () => {
  emit("add", selectRef.value.value);
};
</script>

<style scoped lang="css">
.header {
  font-weight: bold;
}
.content {
  display: flex;
  flex-direction: column;
  padding: 20px;
  gap: 20px;
}
.detail {
  padding: 10px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.field {
  display: flex;
  gap: 5px;
}
.title {
  font-weight: bold;
}
.add {
  display: flex;
  gap: 10px;
}
</style>
