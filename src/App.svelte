<script>
  import data from "./lib/movies";
  import Modal from "./lib/components/Modal.svelte";
  import Movies from "./lib/components/Movies.svelte";
  import Event from "./lib/components/Event.svelte";
  import SearchBar from "./lib/components/SearchBar.svelte";

  // data 사본 추가 (검색기능용)
  let data_temp = [...data];

  const handleLike = (id) => {
    // 원본데이터에서 해당 id에 해당하는 like 값 증가시키기
    data.map((movie) => {
      if (movie.id === id) {
        movie.likeCount += 1;
      }
    });

    // data_temp 있는 내용만 필터링해서 복사
    data_temp = data.filter((movie) => {
      return data_temp.includes(movie);
    });
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

  /* 검색 기능 */
  let alertText = "";
</script>

<!-- <div class={isEvent ? "event show" : "event"}> -->
{#if isEvent}
  <Event bind:isEvent />
{/if}

<SearchBar {data} bind:data_temp bind:alertText />

<!-- 전체보기 버튼 추가 -->
<div class="container">
  <button
    onclick={() => {
      data_temp = [...data]; // 복사본으로 초기화
      alertText = ""; // 검색결과 초기화
    }}>전체보기</button
  >
</div>

<Movies {data_temp} bind:isModal {handleMovieNumber} {handleLike} />

{#if isModal}
  <!-- 단방향props바인딩 : <자식컴포넌트이름 props명={전달값|변수명} /> -->
  <!-- svelte는 간결함을 지향하기 때문에, 전달값(속성명)과 변수명을 일반적으로 동일하게 사용하고, props명 없이 {변수명} 으로 사용함 -->
  <!-- 양방향바인딩 : bind:변수명 -->
  <!-- 자식에게 함수 전달 시 : props함수명={함수명} -->
  <Modal {data} {selectedMovie} {closeModal} />
{/if}

<style>
  .container {
    text-align: center;
  }
</style>
