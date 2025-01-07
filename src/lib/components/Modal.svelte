<script>
    export let data; // props 변수 선언 : 영화데이터
    export let selectedMovie; // props 변수 선언 : 선택한 영화 인덱스
    // export let isModal; // ✏️양방향바인딩으로 부모에게 값 전달할 때 사용
    export let closeModal; // 함수 전달 받음
</script>

<div class="modal">
    <div class="inner">
        <h3>{data[selectedMovie].title}</h3>
        <p>{@html data[selectedMovie].story}</p>
        <!-- <br>이 문자로 들어간 경우 innerHTML 실행하고 싶을 때, @html -->
        <!-- <button class="btn-close" onclick={() => {isModal = false;})}>닫기</button> ✏️양방향바인딩으로 부모에게 값 전달시시-->
        <button class="btn-close" onclick={closeModal}>닫기</button>
    </div>
</div>

<!-- <자식컴포넌트이름 props명={전달값|변수명} /> -->
<style>
    /* Modal 관련 */
    .modal {
        background: rgba(0, 0, 0, 0.7);
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
        background-color: #fff;
        width: 80%;
        padding: 20px;
        border-radius: 10px;
    }
</style>
