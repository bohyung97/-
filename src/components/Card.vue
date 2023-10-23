<template>
  <div class="card">
    <a href="" @click.prevent>
      <img v-if="movie.backdrop_path" v-bind:src="'https://www.themoviedb.org/t/p/w600_and_h900_bestv2/'+ movie.backdrop_path" alt="">
      <img v-else src="https://placehold.it/200x300?text=MoviePoster" alt="">
      <h3>{{ movie.title }}</h3>
    </a>
  </div>
</template>

<script>
export default {
  props:['movie']
}
</script>

<style lang="scss" scoped>
$tablet: '(max-width:860px)';
$mobile: '(max-width:600px)';
.card {
  width: 25%;
  padding: 0px 16px;
  margin-bottom: 16px;

  @media #{$tablet}{
    width: 33.33%;
  }

  @media #{$mobile}{
    width: 50%;
  }

  img {
    width: 100%;
    height: 300px;
    object-fit: cover;
    border-radius: 16px;
    box-shadow: 0px 4px 8px rgba(0,0,0,0.15);
  }

  h3 {
		padding: 16px;
		color: #313131;
		transition: .4s;
	}

	&:hover {
		img {
			transform: scale(1.05);
		}

		h3 {
			color: #24C444;
		}
	}
}

</style>