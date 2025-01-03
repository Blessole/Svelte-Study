<script>
  import logo1 from "./assets/svelte.svg";
  let logo2 = "/vite.svg";
  let title = "영화제목1";
  let year = 2024;
  let category = "로맨스";
  let textRed = "color: red;";

  const data = [
    {
      title: "고질라 X 콩 : 뉴 엠파이어",
      year: 2024,
      category: "어드벤처, 액션, SF",
    },
    {
      title: "듄: 파트2",
      year: 2024,
      category: "액션",
    },
  ];
</script>

<main>
  <h1>영화정보</h1>
  <img src={logo1} alt="" />
  <img src={logo2} alt="" />
  <div>
    <h3 class="bg-yellow" style={textRed}>{title}</h3>
    <p>개봉 : {year}</p>
    <p>장르 : {category}</p>
    <p>{"hello".toUpperCase()}</p>
  </div>
  {#each data as movie, i}
    <!-- content here -->
    <h3 class="bg-yellow" style={textRed}>{i + 1} : {movie.title}</h3>
    <p>개봉 : {movie.year}</p>
    <p>장르 : {movie.category}</p>
  {/each}
</main>

<style>
  .bg-yellow {
    background: gold;
    padding: 10px;
  }
</style>
