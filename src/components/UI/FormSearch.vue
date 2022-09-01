<template>
    <div class="header_sort">
        <form class="header_img_search" @submit.prevent>
            <img class="img_png" src='@/png/Vector.png' alt="">
            <input 
                class="my_input"
                v-model='formSerchQuery'
                @input="$emit('formSerchQuery', formSerchQuery)"
                placeholder="Поиск имени, статуса или даты"
                type="text"
            >
        </form>
        <div>
            <span>Сортировка по: </span>
            <select 
                v-model="modelValue" 
                @change="$emit('sortFilter', modelValue)"
            >
                <option disabled value="">Выбери</option>
                <option 
                    v-for="filter in filterForm" 
                    :key='filter.value'
                >
                    {{filter.title}}
                </option>
            </select>
        </div>
    </div>
</template>

<script>
    export default {
         data() {
            return {
                filterForm: [
                    {title: 'Дата -'},
                    {title: 'Дата +'},
                    {title: 'Выполнено'},
                    {title: 'В работе'}
                ],
                modelValue:'',
                formSerchQuery: null,
            }
        },  
}
</script>

<style  scoped>
.header_sort {
  display: flex;
  justify-content: space-between;
  margin-top: 34px;
}

.img_png {
  width: 18px;
  height: 18px;
  margin-right: 16px;
  margin-left: 40px;
}

.header_img_search {
  display: flex;
  align-items: center;
}

.my_input {
  border: none;
  width: 227px;
  height: 16px;
  font-size: 14px;
}
.my_input::-webkit-input-placeholder {
  color: #C4C4C4;
}

select {
    border: none;
}
</style>