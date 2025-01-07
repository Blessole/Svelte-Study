<script>
  import data from "./lib/movies";
  import Modal from "./lib/components/Modal.svelte";
  import Movies from "./lib/components/Movies.svelte";
  import Event from "./lib/components/Event.svelte";
  import SearchBar from "./lib/components/SearchBar.svelte";
  import { onDestroy, onMount } from "svelte";

  // 이벤트 텍스트
  const eventText = ["영화 정보 업데이트", "신규 영화 추가", "이벤트 진행 중"];

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

  /* 이벤트 기능 (LifeCycle 활용해서 만들기) */
  // 이벤트 창 표시
  let isEvent = true;
  // 이벤트 배열 번호 증가
  let eventIndex = 0;
  let intervalEventText;
  onMount(() => {
    // 일정시간 경과 후 eventIndex를 1 증가 -> 이벤트 문구 자동 변경되도록
    // 3초 지나면 이벤트 인덱스가 1 증가
    intervalEventText = setInterval(() => {
      eventIndex += 1;

      if (eventIndex >= eventText.length) {
        eventIndex = 0;
      }
    }, 3000);
  });

  // 인터벌을 제거해주지 않으면, 컴포넌트가 없어지더라도 메모리에 계속 남아서 실행 됨
  onDestroy(() => {
    // 이벤트 인터벌 제거
    // clearInterval(interval 이름)
    clearInterval(intervalEventText);
  });

  /* 이벤트 기능 (Reactive 문법 사용해서 만들기) */
  //eventIndex 값이 증가하면서 변화하니까 이를 Catch해서 실행하게 됨
  $: {
    // 이벤트 인터벌 제거
    clearInterval(intervalEventText);

    // 일정시간 경과 후 eventIndex를 1 증가 -> 이벤트 문구 자동 변경되도록
    // 3초 지나면 이벤트 인덱스가 1 증가
    intervalEventText = setInterval(() => {
      eventIndex += 1;

      if (eventIndex >= eventText.length) {
        eventIndex = 0;
      }
    }, 3000);
  }

  /* 검색 기능 */
  let alertText = "";
</script>

<!-- <div class={isEvent ? "event show" : "event"}> -->
{#if isEvent}
  <Event bind:isEvent {eventText} {eventIndex} />
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
