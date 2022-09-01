<template>
    <div>
        <div class="cotnent_list">
            <div class="content_block_1">
                <div class="block_ready">
                </div>
                <div class="block_content block">
                    Описание
                </div>
            </div>
            <div class="content_block_2 line">
                <div class="block_status block">
                   Статус
                </div>
                <div class="block_date block">
                    Дата
                </div>
            </div>
        </div>
        <transition-group name="slide-fade">
            <div 
                class="cotnent_list"
                v-for="post in sortPost"
                :key='post.id'
            >
                <div class="content_block_1">
                    <div class="block_ready">
                        <div class="block_btn" @click='$emit("btnPost", post)'>
                            <img 
                                @click='$emit("removePost", post)'
                                class="img_basket"
                                src="../png/pngegg.png" 
                                lt="-"
                            >
                            <div v-if="post.ready === true" class="btn_ready _ready">
                                <span class="span_ready" v-if="post.ready === true"></span>
                                <span v-else></span>
                            </div>
                            <div v-else class="btn_ready">
                                <span class="span_ready" v-if="post.ready === true"></span>
                                <span v-else></span>
                            </div>
                        </div>
                    </div>
                    <div class="block_content">
                        {{post.title}}
                        
                    </div>
                </div>
                <div class="content_block_2">
                    <div class="block_status">
                        <transition name="no-mode-fade">
                            <div class="status_switch_1"
                                v-if="post.ready === false"
                            >
                                {{post.readyText}}
                            </div>
                            <div 
                                class="status_switch_2"
                                v-else
                            >
                                  {{post.readyText}}
                            </div>
                        </transition>
                    </div>
                    <div class="block_date">
                        {{post.showDate}}
                    </div>
                </div>
            </div>
        </transition-group>
    </div>
</template>

<script>
    export default {
        props: {
            sortPost: {
                type: Array
            }
        },
       
    }
</script>

<style scoped>
.block_btn {
    display: flex;
    position: absolute;
    margin-left: 40px;
}

.block {
    position: relative;
}

.block::before {
    position: absolute;
    width: 1px;
    height: 32px;
    left: -20px;
    top: -8px;
    content: '';
    background-color: #C4C4C4;
}

.span_ready:after {
    position: absolute;
    content: '\2713';
    top: 0px;
    left: 20%;
    color:#134EC1;
}

.btn_ready {
    position: relative;
    width: 20px;
    height: 20px;
    border: 1px solid #16191D;
    border-radius: 20px;
    margin-left: 20px;
    cursor: pointer;
}

._ready {
    border: 1px solid #134EC1;
}

.cotnent_list {
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid #EEEBE9;
    height: 58px;
    align-items: center;
}

.content_block_1 {
    display: flex;
}

.block_content {
    width: 340px;
    margin-left: 137px;
}
.content_block_2 {
    display: flex;
    
}
.block_status {
    width: 75px;
    margin-right: 76px;
    
}
.block_date {
    width: 75px;
    margin-right: 32px;
}

.status_switch_1 {
    position: absolute;
    color: #134EC1;
}

.status_switch_2 {
    position: absolute;
    color: #F89B11;
}


.no-mode-fade-enter-active, .no-mode-fade-leave-active {
  transition: opacity .4s
}

.no-mode-fade-enter-from, .no-mode-fade-leave-to {
  opacity: 0
}


.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.3s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}

.img_basket {
    width: 22px;
    cursor: pointer;
}
</style>