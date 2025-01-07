<script>
  import data from "./lib/movies";
  import Modal from "./lib/components/Modal.svelte";

  let likeCount = 0; // 좋아요 수를 저장할 변수
  const handleLike = (i) => {
    data[i].likeCount += 1;
    console.log(likeCount);
  };

  let isModal = false; // 모달창 변수 추가

  let selectedMovie = 0; // 선택한 영화의 Index 변수 추가

  const closeModal = () => {
    isModal = false;
  };
</script>

<main class="container">
  <h1>영화정보</h1>
  {#each data as movie, i}
    <div class="item">
      <figure>
        <img src={movie.imgUrl} alt={movie.title} />
      </figure>
      <div class="info">
        <h3 class="bg-yellow">{movie.title}</h3>
        <p>개봉 : {movie.year}</p>
        <p>장르 : {movie.category}</p>
        <button
          onclick={() => {
            handleLike(i);
          }}>좋아요 {movie.likeCount}</button
        >
        <button
          class="btn btn-primary"
          onclick={() => {
            isModal = true;
            selectedMovie = i;
          }}>상세보기</button
        >
      </div>
    </div>
  {/each}
</main>

{#if isModal}
  <!-- 단방향props바인딩 : <자식컴포넌트이름 props명={전달값|변수명} /> -->
  <!-- svelte는 간결함을 지향하기 때문에, 전달값(속성명)과 변수명을 일반적으로 동일하게 사용하고, props명 없이 {변수명} 으로 사용함 -->
  <!-- 양방향바인딩 : bind:변수명 -->
  <!-- 자식에게 함수 전달 시 : props함수명={함수명} -->
  <Modal {data} {selectedMovie} {closeModal} />
{/if}

<style>
  .bg-yellow {
    background: gold;
    padding: 10px;
    color: #333;
  }

  .item {
    width: 100%;
    border: 1px solid #ccc;
    display: flex;
    margin-bottom: 20px;
    padding: 1rem;
  }

  .item figure {
    width: 30%;
    margin-right: 1rem;
  }

  .item img {
    width: 100%;
  }

  .item .info {
    width: 100%;
  }
</style>
