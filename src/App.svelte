<script>
  import data from "./lib/movies";
  let likeCount = 0; // 좋아요 수를 저장할 변수
  const handleLike = (i) => {
    data[i].likeCount += 1;
    console.log(likeCount);
  };

  let isModal = false; // 모달창 변수 추가

  let selectedMovie = 0; // 선택한 영화의 Index 변수 추가가
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
  <div class="modal">
    <div class="inner">
      <h3>{data[selectedMovie].title}</h3>
      <p>{@html data[selectedMovie].story}</p>
      <!-- <br>이 문자로 들어간 경우 innerHTML 실행하고 싶을 때, @html -->
      <button
        class="btn-close"
        onclick={() => {
          isModal = false;
        }}>닫기</button
      >
    </div>
  </div>
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
