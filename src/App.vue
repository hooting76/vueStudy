<!-- template <= html 코드가 작성되는 구간-->
<!-- asset 폴더 <= 이미지 || 자원 류 저장 공간 -->
<!-- components 폴더 <= 재사용 컴포넌트 위치 -->
<!-- main.js <= 애플리케이션의 중심 -->

 <!-- html에 데이터를 넣는것 : 데이터 바인딩 -->
<template>
  <NavBar/><!-- 불러온 컴포넌트 사용 -->
  <Event :text="text" /> <!-- props 사용 예시 / 속성명(props 변수) = "보낼 값"-->

  <SearchBar 
    :data="data_temp" 
    @searchPhoto="searchPhoto($event)"
  />

  <p>
    <button @click="showAllPhoto">전체보기</button>
  </p>

  <!-- 파라미터에서 전달받은 값을 $event로 받을 수 있다  -->
  <Photos 
    :data="data_temp" 
    @openModal="isModal=true; selectedPhoto=$event"
    @increaseLike="increaseLike($event)"
  />

  <!-- App에서는 하위 Modal 에서 온 closeModal 요청을 @로 받음-->
  <!-- 이후 "" 안에 처리할 로직을 넣어서 처리 -->
  <Modal 
    :data="data" 
    :isModal="isModal" 
    :selectedPhoto="selectedPhoto" 
    @closeModal="isModal=false"
  />

</template>

<script>
  import data from "./assets/photos"; // 사진 데이터 import
  import NavBar from "./components/NavBar.vue"; // 컴포넌트 import
  import Modal from "./components/Modal.vue"; // 컴포넌트 import
  import Event from "./components/Event.vue";
  import Photos from "./components/Photos.vue";
  import SearchBar from "./components/SearchBar.vue";

  export default {
    name: 'App',
    data(){
      return{
        isModal: false,
        data: data, // 원본 데이터
        data_temp: [...data], // 사본 데이터 // ...이 원래 있던 데이터를 복사해온다는 뜻
        selectedPhoto: 0,
        text: '광기와 우울의 시시한 연애?!',
      }
    },
    methods: {
      // 여기에 함수 추가 가능
      increaseLike(id){
        // this를 선언해줘야지만, 객체 내의 like를 찾는다.
        // this.data[index].like += 1;
        this.data.find(photo =>{
          if(photo.id == id) {
            photo.like += 1;
          }
        })
      },
      searchPhoto(title){
        // 사진 제목이 포함된 데이터를 가져옴
        this.data_temp = this.data.filter(photo =>{
          return photo.title.includes(title);
        })
      },
      showAllPhoto(){
        this.data_temp = [...this.data];
      }
    },
    // 컴포넌트 등록 
    components: {
      NavBar: NavBar,
      Modal: Modal,
      Event: Event,
      Photos: Photos,
      SearchBar,
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
