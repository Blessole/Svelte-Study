<script>
  const data = [
    {
      title: "고질라 X 콩 : 뉴 엠파이어",
      year: 2024,
      category: "어드벤처, 액션, SF",
      likeCount: 0,
    },
    {
      title: "듄: 파트2",
      year: 2024,
      category: "액션",
      likeCount: 0,
    },
  ];

  let likeCount = 0; // 좋아요 수를 저장할 변수
  const handleLike = (i) => {
    data[i].likeCount += 1;
    console.log(likeCount);
  };
</script>

<main>
  <h1>영화정보</h1>
  {#each data as movie, i}
    <!-- content here -->
    <h3 class="bg-yellow">{movie.title}</h3>
    <p>개봉 : {movie.year}</p>
    <p>장르 : {movie.category}</p>
    <button
      onclick={() => {
        handleLike(i);
      }}>좋아요 {movie.likeCount}</button
    >
  {/each}
</main>

<style>
  .bg-yellow {
    background: gold;
    padding: 10px;
    color: #333;
  }
</style>
