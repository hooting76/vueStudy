<template>
    <div class="search-box">
        <!-- @input="inputText = $event.target.value"  방식으로 input을 컨트롤 할 수 있긴 하다. -->
        <!-- v-model="변수" // 사용자에게 입력받은 값을 변수에 알아서 저장해준다. 다만 입력하나마다 예민하게 반응한다.-->
        
        <input 
            type="search" 
            @change="
                $emit('searchPhoto', $event.target.value)
                inputText = $event.target.value;
                $event.target.value = ''
            "
            placeholder="검색어 입력"
        />
        <button>검색</button>
    </div>
    <p>{{ inputText }}</p>
</template>

<script>
// watch 는 특정 상태변수가 변경됨을 감지하는 hook의 종류
// hook <- 가로챔을 의미
export default {
    name: "SearchBarComponent",
    data() {
        return {
            inputText: '',
        }
    },
    props: {
        data: Array,
    },
    watch: {
        inputText(name){
            // 입력한 사진 제목이 데이터에 있는지 확인
            // name은 매개변수일 뿐이고, inputText의 변화를 감지한다.
            const findName = this.data.filter(Photo => {
                // 여기서 Photo는 매개변수임
                return Photo.title.includes(name);
            })
            
            if(findName.length == 0){
                alert('해당 자료가 없습니다.');
            }
        }
    }
}
</script>

<style>
    .search-box{
        padding: 10px;
        display: flex;
        justify-content: center;
    }
    .search-box input{
        padding: 5px 10px;
    }
    .search-box button{
        margin: 0;
    }
</style>