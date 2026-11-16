<template>
  <div class="modal" v-if="isModal">
    <div class="inner">
      <h3>{{ data[selectedPhoto].title }}</h3>
      <p>사진 상세정보</p>
        <!-- 자식은 부모에게 이벤트를 요청해야 함. -->
        <!-- 그럴땐 $emit() 을 사용하여 커스텀 이벤트 전달-->
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name: "ModalComponent",
    props: {
        data: Array,
        isModal: Boolean,
        selectedPhoto: Number,
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
    }

    .event p{
        margin: 0;
    }
</style>