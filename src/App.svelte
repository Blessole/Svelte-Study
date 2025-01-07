<script>
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
</script>

<Movies {data} bind:isModal {handleMovieNumber} {handleLike} />

{#if isModal}
  <!-- 단방향props바인딩 : <자식컴포넌트이름 props명={전달값|변수명} /> -->
  <!-- svelte는 간결함을 지향하기 때문에, 전달값(속성명)과 변수명을 일반적으로 동일하게 사용하고, props명 없이 {변수명} 으로 사용함 -->
  <!-- 양방향바인딩 : bind:변수명 -->
  <!-- 자식에게 함수 전달 시 : props함수명={함수명} -->
  <Modal {data} {selectedMovie} {closeModal} />
{/if}

<style>
</style>
