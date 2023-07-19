<template>
    <form
        class="h-full flex flex-col justify-between"
        @submit="handleSubmit"
    >
        <h1 class="mt-8 mb-3 text-4xl font-bold text-center font-custom">Редактирование данных</h1>

        <select
            name="element"
            class="mb-4 py-2 px-3 bg-transparent border border-black focus:border-blue-500 focus:outline-none rounded-md cursor-pointer font-Inter"
            v-model="selectedItemValue"
        >
            <option value="" autofocus>Выберите элемент</option>
            <option
                v-for="(item) in items"
                v-bind:value="item.value"
            >
              {{ item.name }}
            </option>
        </select>

        <input
            name="elementsInput"
            type="text"
            class="mb-6 py-2 px-4 w-25 border outline-0 focus:ring-1 focus:ring-blue-500 rounded-md font-Inter"
            id="elementsInput"
            :value="selectedItemValue"
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

    const newData = initialData.map((item, i) => ({
        ...item,
        _id: i
    }));

    export default {
        data() {
            return {
                items: newData,
                selectedItemValue: '',
                selectedItemId: undefined,
                changedValue: ''
            };
        },
        methods: {
            handleInput(evt) {
                const selectedItem = this.items.find(item => item.value === this.selectedItemValue);
                selectedItem && (this.selectedItemId = selectedItem._id);
                this.changedValue = evt.target.value;
            },

            handleSubmit(evt) {
                evt.preventDefault();
                const selectedItem = this.items.find(item => item._id === this.selectedItemId);
                selectedItem && (selectedItem.value = this.changedValue);
                this.selectedItemValue = '';
                this.selectedItemId = undefined;
                this.changedValue='';
            }
        },
    };
</script>

<style scoped></style>
