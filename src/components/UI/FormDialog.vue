<template>
    <div class="form_dialog" v-if="show" @click="hidenFormDialog">
        <div @click.stop class="form_content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            show: {
                type: Boolean
            }
        },
        methods: {
            hidenFormDialog(){
                this.$emit('update:show', false);
            }
        }
    }
</script>

<style scoped>
.form_dialog {
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    background: rgba(0, 0, 0, .5);
    backdrop-filter: blur(4px);
    position: fixed;
    display: flex;
    z-index: 10;
}
.form_content {
    margin: auto;
    background: #fff;
    border-radius: 8px;
}
</style>