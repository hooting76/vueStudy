<template>
    <div class="container">
        <h1>사진 정보</h1>
        <!-- 뷰 문법 반복문으로 데이터 바인딩 -->
        <!-- :key="i" : 인덱스 번호 지정하는거라 이해하자 -->
        <div v-for="(photo) in data" :key="photo.id" class="item">
            <figure>
            <img 
                :src="`${photo.imgPath}`" 
                :alt="`${photo.title}`" />
            </figure>

            <div class="info">
                <h2 class="bg-yellow" :style="photo.textRed">
                    {{ photo.title }}
                </h2>
                <p>촬영일: {{ photo.year }}</p>
                <p>장소: {{ photo.location }}</p> 

                <!-- 좋아요 버튼 이벤트 -->
                <!-- v-on:이벤트명="실행코드" 로 동작 -->
                <!-- v-on 대신 @ 로 축약 가능 -->
                <button @:click="$emit('increaseLike',photo.id)">좋아요</button> 
                <span>{{ photo.like }}</span>

                <p>
                    <!-- $emit(이름, 전달할 값) 형태로 요청 -->
                    <!-- 2번째 인자에 인덱스 번호를 전달합니다. -->
                    <button 
                        @click="$emit('openModal', photo.id)">상세보기</button>
                </p>
            </div>
        </div>        
    </div>
</template>

<script>
export default {
    name: "PhotosComponent",
    props: {
        data: Array,
    }
}
</script>

<style>
    .container{
        padding: 20px;
    }
</style>