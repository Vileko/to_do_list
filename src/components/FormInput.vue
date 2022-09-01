<template>
    <form @submit.prevent>
       <div class="form_block">
            <div class="top_form">
                <h3>Создать новую задачу</h3>
                <div class="btn_close" @click="$emit('closeForm', form)">
                    <span class="close"></span>
                </div>
            </div>
            <div class="form_description">Описание</div>
            <input 
                class="my_input"
                v-model="post.title"
                type="text" 
                placeholder="Введите описание"
            >
            <div v-if="formValidation === false">
                <span>введите описание</span>
            </div>
            <div class="block_btn">
                <my-btn 
                class="btn"
                @click='addContentPost'
                >
                    Создать
                </my-btn>
            </div>
       </div>
    </form>
</template>

<script>
import MyBtn from './UI/MyBtn.vue';
    export default {
  components: { MyBtn },
        data(){
            return{
                post: {
                    title: ''
                },
                formValidation: true,
            }
        },
        methods: {
            addContentPost(){
                if(this.post.title.length > 0) {
                    this.formValidation = true;
                    this.post.id = Date.now();
                    this.post.ready = false;
                    this.post.readyText = 'В работе';
                    this.post.date= new Date().toISOString().split('T')[0];
                    this.post.showDate = new Date().toLocaleDateString();
                    this.$emit('createPost', this.post);
                    this.post = {
                        title: ''
                    }
                } else {
                    this.formValidation = false;
                }
            },
        }
    }
</script>

<style scoped>
.btn_close {
    position: relative;
    width: 22px;
    height: 22px;
    border-radius: 5px;
    background-color: #314B99;
}

.close {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 22px;
    height: 22px;
    cursor: pointer;
}

.close:before, .close:after {
    position: absolute;
    content: ' ';
    height: 8px;
    width: 1px;
    background-color: rgb(255, 255, 255);
    border-radius: 5px;
}
.close:before {
    transform: rotate(45deg);
}
.close:after {
    transform: rotate(-45deg);
}

form {
    width: 400px;
    height: 281px;
}

.top_form {
    display: flex;
    justify-content: space-between;
    width: 100%;
}

.form_description {
    font-size: 14px;
    font-weight: 400;
    margin-bottom: 5px;
}

.form_block {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 40px;
}
.form_block span {
    font-size: 14px;
}

.my_input {
    padding: 11px 16px;
    border-radius: 5px;
    border: 1px solid #DDE2E4;
    width: 90%;
}

.block_btn {
    display: flex;
    width: 100%;
    justify-content: center;
    margin-top: 30px;
}

.btn {
    font-weight: 400;
    font-size: 18px;
    color: #314B99;
}

h3 {
    font-weight: 700;
    font-size: 18px;
    margin-bottom: 30px;
}

span {
    color: rgb(189, 189, 189)
}
</style>