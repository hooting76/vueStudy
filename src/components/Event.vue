<template>
    <!-- 참일때 show 값이 true / 거짓일 때 show 값은 false 로 하여서 클래스를 동적으로 다룬다-->
    <div class="event" :class="{show : isOpen}">
        <p>{{ text }}</p>
        <button @click="isOpen=false">X</button>
    </div>
</template>

<script>
export default {
    name: 'EventComponent',
    // props를 받을때 타입 검증을 해야함
    props: {
        text: String,
    },
    data(){
        return {
            isOpen: true
        }
    }
}
</script>

<style>
    .event{
        background: #444;
        color: #fff;
        padding: 10px 20px;
        text-align: center;
        font-size: small;
        display: flex;
        justify-content: space-between;
        align-items: center;
        display: none;
    }

    .show{
        display: flex;
    }

    .event p{
        margin: 0;
    }
    .event button{
        margin: 0;
    }
</style>