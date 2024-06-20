<template>
  <v-container>
    <v-row>
      <v-col cols="4">
        <v-select
          label="Выберите поле для добавления"
          :items="['Текстовое поле', 'Текстовая область', 'Файл']"
          v-model="selectType"
          variant="outlined"
        ></v-select>
        <v-select
          label="Кол-во колонок"
          :items="[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]"
          v-model="numOfColumn"
          variant="outlined"
        ></v-select>
        <v-text-field
          label="Подпись"
          variant="outlined"
          v-model="labelField"
        ></v-text-field>
        <v-btn
          variant="tonal"
          class="button-add"
          @click="addToForm(selectType, numOfColumn, labelField)"
        >
          Добавить на форму
        </v-btn>
      </v-col>
      <v-col cols="8">
        <v-row>
          <template v-for="(items, i) in formData" :key="i">
            <template v-if="items.type === 'Текстовое поле'">
              <v-col :cols="items.cols">
                <v-text-field
                  :label="items.label"
                  variant="outlined"
                ></v-text-field>
              </v-col>
            </template>
            <template v-else-if="items.type === 'Текстовая область'">
              <v-col :cols="items.cols">
                <v-textarea :label="items.label" variant="outlined"></v-textarea>
              </v-col>
            </template>
            <template v-else-if="items.type === 'Файл'">
              <v-col :cols="items.cols">
                <v-file-input :label="items.label" variant="outlined"></v-file-input>
              </v-col>
            </template>
          </template>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";

export default defineComponent({
  setup() {
    const formData = reactive<any>([]);
    const selectType = ref<string>("Текстовое поле");
    const numOfColumn = ref<number>(12);
    const labelField = ref<string>("");
    const genForm = ref<boolean>(false);

    const addToForm = (type: string, cols: number, label: string) => {
      formData.push({ type, cols, label });
    };

    return {
      formData,
      selectType,
      addToForm,
      numOfColumn,
      labelField,
      genForm,
    };
  },
});
</script>

<style lang="scss" scoped>
.button-add {
  margin-right: 10px;
}
</style>
