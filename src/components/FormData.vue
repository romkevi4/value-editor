<template>
    <form
        class="h-full flex flex-col justify-between"
        @submit="handleSubmit"
    >
        <h1 class="mt-8 mb-3 text-4xl font-bold text-center font-custom">Редактирование данных</h1>

        <select
            name="element"
            class="mb-4 py-2 px-3 bg-transparent border border-gray-500 focus:border-blue-500 focus:outline-none rounded-md cursor-pointer font-Inter"
            v-model="selectedItemValue"
        >
            <option value="" autofocus>Выберите элемент</option>
            <option
                :value="item"
                :key="item.id"
                v-for="(item) in items"
            >
              {{ item.name }}
            </option>
        </select>

        <input
            name="elementsInput"
            type="text"
            class="mb-6 py-2 px-4 w-25 border outline-0 focus:ring-1 focus:ring-blue-500 rounded-md font-Inter"
            id="elementsInput"
            :value="selectedItemValue.value"
            @input="handleInput"
        >

        <button
            type="submit"
            class="w-full h-16 bg-transparent border border-blue-500 rounded-md hover:bg-blue-500 text-3xl font-Inter"
        >
          Отправить
        </button>
    </form>
</template>

<script>
    import { initialData } from '../utils/initialData';

    export default {
        data() {
            const newData = initialData.map((item, i) => ({
              ...item,
              id: i
            }));

            return {
                items: newData,
                selectedItemValue: '',
                selectedItemId: undefined
            };
        },
        methods: {
            handleInput(evt) {
              console.log(evt.target.value);
              this.selectedItemValue = evt.target.value;
              this.selectedItemId = evt.target.value.id;
            },

            handleSubmit(evt) {
                evt.preventDefault();

                console.log(this.selectedItemId);
                const selectedItem = this.items.find(item => item.id === this.selectedItemId);
                // console.log(selectedItem);
                // console.log(this.selectedItemValue);

                selectedItem && (selectedItem.value = this.selectedItemValue);
                this.selectedItemValue = '';
                this.selectedItemId = undefined;
            }
        },
    };
</script>

<style scoped></style>