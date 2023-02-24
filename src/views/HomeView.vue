<template>
  <div class="home">
		
		<div class="feature-card">
			<router-link to="/movie/tt0409591">
				<img src="https://www.thebanner.org/sites/default/files/styles/social_media_thumbnail/public/MM-479%20Ted%20Lasso.jpg?itok=zdUrJnl3" alt="Ted Lasso Poster" class="feature-img" />
				<div class="detail">
					<h3>Ted Lasso</h3>
					<p>American college football coach Ted Lasso heads to London to manage AFC Richmond, a struggling English Premier League football team.</p>
				</div>
			</router-link>
		</div>
		
		<form @submit.prevent="SearchMovies()" class="search-box">
			<input type="text" placeholder="What are you looking for?" v-model="search"/>
			<input type="submit" value="Search" />
		</form>

		<div class="movies-list">MOVIES</div>

  </div>
</template>

<script>
import { ref } from 'vue';
import env from '@/env.js';

export default {
	setup () {
		const search = ref("");
		const movies = ref([]);

		const SearchMovies = () => {
			if (search.value != "") {
				// console.log(search.value); -> testing
				fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
					.then(response => response.json())
					.then(data => {
						console.log(data);
					})
			}
		}

		return {
			search,
			movies,
			SearchMovies,
		}
	}
}
</script>

<style lang="scss">
.home{
	.feature-card {
		position: relative;

		.feature-img {
			display: block;
			width: 100%;
			height: 300px;
			object-fit: cover;

			position: relative;
			z-index: 0;
		}

		.detail {
			position: absolute;
			left: 0;
			right: 0;
			bottom: 0;
			background-color: rgba(0, 0, 0, 0.6);
			padding: 16px;
			z-index: 1;

			h3 {
				color: #fff;
				margin-bottom: 16px;
			}

			p {
				color: #fff;
			}
		}
	}

	.search-box {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 16px;

		input {
			display: block;
			appearance: none;
			border: none;
			outline: none;
			background: none;

			&[type="text"] {
				width: 100%;
				color: #fff;
				background-color: #496583;
				font-size: 20px;
				padding: 10px 16px;
				border-radius: 8px;
				margin-bottom: 15px;
				transition: 0.4s;

				&::placeholder {
					color: #f3f3f3;
				}

				&:focus {
					box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
				}
			}

			&[type="submit"] {
				width: 100%;
				max-width: 300px;
				background-color: #42B883;
				padding: 16px;
				border-radius: 8px;
				color: #FFF;
				font-size: 20px;
				text-transform: uppercase;
				transition: 0.4s;

				&:active {
					background-color: #3B8070;
				}
			}
		}
	}
}
</style>