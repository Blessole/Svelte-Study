<script>
  const data = [
    {
      title: "엘리멘탈",
      year: 2023,
      category: "어린이, 로맨스",
      likeCount: 0,
      imgUrl: "/images/elemental_poster.jpg",
    },
    {
      title: "하얼빈",
      year: 2024,
      category: "액션, 범죄",
      likeCount: 0,
      imgUrl: "/images/haerbin_poster.jpg",
    },
    {
      title: "알라딘",
      year: 2019,
      category: "어린이, 뮤지컬",
      likeCount: 0,
      imgUrl: "/images/aladin_poster.jpg",
    },
  ];

  let likeCount = 0; // 좋아요 수를 저장할 변수
  const handleLike = (i) => {
    data[i].likeCount += 1;
    console.log(likeCount);
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
      </div>
    </div>
  {/each}
</main>

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
