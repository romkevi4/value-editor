<template>
    <form>
        <h1 class="mb-3 text-4xl font-bold text-center mt-8">Редактирование данных</h1>

        <select
            name="element"
            class="h-full bg-transparent border border-gray-500 focus:border-blue-500 focus:outline-none mr-2 mb-2 py-2 px-4 rounded-md cursor-pointer"
            v-model="selectedItemValue"
        >
            <option value="" autofocus>Выберите элемент</option>
            <option
                :value="item.value"
                :key="index"
                v-for="(item, index) in items"
            >
              {{ item.name }}
            </option>
        </select>

        <input
            name="elementsInput"
            type="text"
            class="h-full border py-2 px-4 mb-2 w-25 outline-0 rounded-md focus:ring-1 focus:ring-blue-500"
            id="elementsInput"
            v-model="selectedItemValue"
        >
    </form>
</template>

<script>
    import { initialData } from '../utils/initialData';

    export default {
        data() {
            return {
                items: initialData,
                selectedItemValue: '',
            };
        },
        // methods: {
        //     selectItem(item) {
        //         this.selectedItem = item;
        //     },
        //     saveChanges() {
        //         this.selectedItem = null; // сброс выбранного элемента
        //     },
        // },
    };
</script>

<style scoped></style>