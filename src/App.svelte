<script>
  import { fade, fly } from "svelte/transition";
  import data from "./lib/movies";
  import Modal from "./lib/components/Modal.svelte";
  import Movies from "./lib/components/Movies.svelte";

  let likeCount = 0; // 좋아요 수를 저장할 변수
  const handleLike = (i) => {
    data[i].likeCount += 1;
  };

  let isModal = false; // 모달창 변수 추가

  let selectedMovie = 0; // 선택한 영화의 Index 변수 추가

  const closeModal = () => {
    isModal = false;
  };

  const handleMovieNumber = (i) => {
    selectedMovie = i;
  };

  // 이벤트 창 표시
  let isEvent = true;
</script>

<!-- <div class={isEvent ? "event show" : "event"}> -->
{#if isEvent}
  <div class="event show" in:fly={{ y: -400, duration: 1000 }} out:fade>
    <p>NETPLIX 강렬한 운명의 드라마, 경기크리처</p>
    <button
      onclick={() => {
        isEvent = false;
      }}>X</button
    >
  </div>
{/if}
<button
  onclick={() => {
    isEvent = true;
  }}>이벤트 창 나타나기</button
>
<Movies {data} bind:isModal {handleMovieNumber} {handleLike} />

{#if isModal}
  <!-- 단방향props바인딩 : <자식컴포넌트이름 props명={전달값|변수명} /> -->
  <!-- svelte는 간결함을 지향하기 때문에, 전달값(속성명)과 변수명을 일반적으로 동일하게 사용하고, props명 없이 {변수명} 으로 사용함 -->
  <!-- 양방향바인딩 : bind:변수명 -->
  <!-- 자식에게 함수 전달 시 : props함수명={함수명} -->
  <Modal {data} {selectedMovie} {closeModal} />
{/if}

<style>
  .event {
    width: 100%;
    background-color: #666;
    padding: 5px 1em;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: white;
    text-align: center;
    margin-bottom: 1em;

    /* 창이 보이지 않게 */
    max-height: 0;
    opacity: 0;
    overflow: hidden;
    transition: all 0.4s;
  }

  /* 기본 : 창이 보이게 */
  .show {
    opacity: 1;
    max-height: 100px;
  }
  .event button {
    padding: 2px;
  }
</style>
