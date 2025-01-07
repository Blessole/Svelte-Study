<script>
    export let data_temp = []; // 기본 값이 배열형식이라 []
    export let isModal = false;
    export let handleLike;
    // export let selectedMovie = 0; // 값에 바로 바인딩
    export let handleMovieNumber; // 함수를 활용해서 바인딩

    // TODO : 좋아요 값이 바로 업데이트가 안되는 문제가 있음
</script>

<main class="container">
    <h1>영화정보</h1>
    {#each data_temp as movie}
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
                        handleLike(movie.id);
                    }}>좋아요 {movie.likeCount}</button
                >
                <button
                    class="btn btn-primary"
                    onclick={() => {
                        isModal = true;
                        // selectedMovie = i;
                        handleMovieNumber(movie.id);
                    }}>상세보기</button
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
