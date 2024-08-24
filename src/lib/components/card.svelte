<script>

  import { onMount } from 'svelte';



onMount(() => {

			const apiUrl = `https://api.github.com/users/EmonaSantiago/repos?sort=updated&per_page=50`;

	
	fetch(apiUrl)
		.then((response) => response.json())
		.then((repos) => {
			repos = repos.map((repo) => {
				return {
					...repo,
					name: repo.name.replace(/-/g, ' ') 
				};
			});

			repos = repos.filter((repo) => repo.stargazers_count > 0);

			repos.sort((a, b) => b.stargazers_count - a.stargazers_count);

			const container = document.getElementById('repos-container');
			repos.forEach((repo) => {
				const repository = document.createElement('section');
				repository.className = 'repository';
				repository.innerHTML = `
				
				
					<h3 href="${repo.html_url}" target="_blank" class="repo-name">${repo.name}</h3>
					
					<section class="repo-bio">
						<p>${repo.description || 'No description available.'} </p>
					</section>

					<section class="repo-button">
						<a href="${repo.homepage}" target="_blank" class="live-button"> ${"PROJECT BEKIJKEN" || 'no link available'} </a>
					</section>
				

				
				`;
				container.appendChild(repository);
			});
		})
		.catch((error) => console.error('Error fetching repos:', error));
});


</script>
<ul id="repos-container"></ul>
