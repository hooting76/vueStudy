<template>
    <div class="event">
        <p>{{ text }}</p>
    </div>
</template>

<script>
export default {
    name: 'EventComponent',
    // props를 받을때 타입 검증을 해야함
    props: {
        text: String,
    }
}
</script>

<style>
    
</style>