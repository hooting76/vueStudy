<!-- template <= html 코드가 작성되는 구간-->
<!-- asset 폴더 <= 이미지 || 자원 류 저장 공간 -->
<!-- components 폴더 <= 재사용 컴포넌트 위치 -->
<!-- main.js <= 애플리케이션의 중심 -->

 <!-- html에 데이터를 넣는것 : 데이터 바인딩 -->
<template>
  <h1>사진 정보</h1>

  <!-- 뷰 문법 반복문으로 데이터 바인딩 -->
  <!-- :key="i" : 인덱스 번호 지정하는거라 이해하자 -->
  <div v-for="(photo, i) in data" :key="i" class="item">
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
      <button @:click="increaseLike(i)">좋아요</button> 
      <span>{{ photo.like }}</span>

      <p>
        <button @click="isModal=true">상세보기</button>
      </p>
    </div>
  </div>

  <div class="modal" v-if="isModal">
    <div class="inner">
      <h3>Detail</h3>
      <p>사진 상세정보</p>
      <button @click="isModal=false">닫기</button>
    </div>
  </div>

</template>


<script>
  export default {
    name: 'App',
    data(){
      return{
        isModal: false,
        data: [
          {
            title: "등대",
            year: 2024,
            location: "정동진",
            textRed: "color: red",
            like: 0,
            imgPath: "./assets/lighthouse.jpg",
          },
          {
            title: "몽환적 경계",
            year: 2024,
            location: "여수", 
            like: 0,
            imgPath: "./assets/mystic.jpg",
          },
          {
            title: "역군",
            year: 2024,
            location: "동해 어달항", 
            like: 0,
            imgPath: "./assets/power.jpg",
          },
          {
            title: "고향가는길",
            year: 2024,
            location: "정동진", 
            like: 0,
            imgPath: "./assets/wayhome.jpg",
          },
        ]
      }
    },
    methods: {
      // 여기에 함수 추가 가능
      increaseLike(index){
        // this를 선언해줘야지만, 객체 내의 like를 찾는다.
        this.data[index].like += 1;
      }
    }
  }
</script>


<style>
  * {
    box-sizing: border-box;
    margin: 0;
  }

  body{
    max-width: 768px;
    margin: 0 auto;
    padding: 20px;
  }

  h1, h2, h3{
    margin-bottom: 1rem;
  }
  
  p{
    margin-bottom: .5rem;
  }
  button{
    margin-right: 10px;
    margin-top: 1rem;
  }

  .item{
    width: 100%;
    border: 1px solid #ccc;
    display: flex;
    margin-bottom: 20px;
    padding: 1rem;
  }

  .item figure{
    width: 30%;
    margin-right: 1rem;
  }

  .item img{
    width: 100%;
  }

  .item .info{
    width: 100%;
  }

  .modal{
    background: rgba(0, 0, 0, .7);
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal .inner {
    background: #fff;
    width: 80%;
    padding: 20px;
    border-radius: 10px;
  }
</style>
