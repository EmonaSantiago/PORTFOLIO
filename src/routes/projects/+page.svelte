<script>
  import Card from "$lib/components/card.svelte";


  import { onMount } from 'svelte';



onMount(() => {

		// GitHub API laat maar 30 zien bij default
		// Verander username
			const apiUrl = `https://api.github.com/users/EmonaSantiago/repos?sort=updated&per_page=50`;

	
	fetch(apiUrl)
		.then((response) => response.json())
		.then((repos) => {
			repos = repos.map((repo) => {
				return {
					...repo,
					name: repo.name.replace(/-/g, ' ') // deze line zorgt ervoor dat er spaties staan ipv - 
				};
			});

				// Haal de volgende regel weg om alle repo's te krijgen op de website, wil je dit niet dan kan je de beste repo's een ster
				// geven zodat je alleen die ziet :) 

			repos = repos.filter((repo) => repo.stargazers_count > 0);

			// Sorteert het werk van hoog naar laag ster

			repos.sort((a, b) => b.stargazers_count - a.stargazers_count);

			const container = document.getElementById('repos-container');
			repos.forEach((repo) => {
				const repository = document.createElement('section');
				repository.className = 'repository';
				repository.innerHTML = `
				
				
					<h3><a href="${repo.html_url}" target="_blank" class="repo-name">${repo.name}</a></h3>
					
					<section class="repo-bio">
						<p>${repo.description || 'No description available.'} </p>
					</section>

					<section class="repo-button">
						<a href="${repo.homepage}" target="_blank" class="live-button"> ${"Live Site" || 'no link available'} </a>
					</section>
				

				
				`;
				container.appendChild(repository);
			});
		})
		.catch((error) => console.error('Error fetching repos:', error));
});


</script>

<div class="container">

	<div class="intro">
		<h2>GITHUB PROJECTS</h2>
	</div>

		<main>
			<div class="content">
				<h1>GITHUB PROJECTS</h1>
				<!-- Import Cards section -->
			<Card></Card>
			</div>

			<a class="button_more" href="/">Ga terug</a>

		</main>
</div>

<section class="github-portfolio">
	<section class="portfolio-title">
		<h2>my work on github ✨</h2>
	</section>
	

	<ul id="repos-container"></ul>
</section>

<style>

.github-portfolio {
	background-color: blue;
}
    * {
	box-sizing: border-box;
	margin: 0;
}

.container {
	background-color: var(--dark-blue);
}

h1 {
	margin: 1rem 0;
	color: var(--dark-blue);
}

h2 {
	color: white;
	opacity: 0;
	font-size: 5rem;
	animation: fadeIn 2s ease forwards;
}

p {
	font-size: 4rem;
	opacity: 0;
	animation: fadeInText 2s ease forwards 3s;
}

.intro {
	height: 100vh;
	display: flex;
	justify-content: center;
	align-items: center;
}

main {
	position: absolute;
	top: 0;
	height: 100vh;
	width: 100%;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	background-color: var(--light-blue);
	transform: scale(0, 0);
	animation: animate 1s ease-in forwards 2s;
	overflow: hidden;
}

.content {
	width: 100%;
	text-align: center;
	overflow-y: auto;
}

@keyframes animate {
	0% {
		transform: scale(0, 0.005);
	}
	50% {
		transform: scaleY(0.005);
	}
	100% {
		transform: scale(1, 1);
	}
}

@keyframes fadeIn {
	from {
		opacity: 0;
		transform: translateY(50%);
	}
	to {
		opacity: 1;
		transform: translateY(-50%);
	}
}

@keyframes fadeInText {
	from {
		opacity: 0;
		transform: translateY(50%);
	}
	to {
		opacity: 1;
		transform: translateY(0%);
	}
}

.btns_more {
	margin-bottom: 2em;
}



</style>

