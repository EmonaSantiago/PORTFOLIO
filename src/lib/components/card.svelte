<script>

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

<!-- <ul class="cards">
    <li>
      <a href="/" class="card">
        <img src="../emona.png" class="card__image" alt="" />
        <div class="card__overlay">
          <div class="card__header">                   
            <img class="card__thumb" src="../emona.png" alt="" />
            <div class="card__header-text">
              <h3 class="card__title">PORTFOLIO</h3>            
              <span class="card__status">endterm assessment</span>
            </div>
          </div>
          <p class="card__description">Welkom op mijn portfolio website!</p>
        </div>
      </a>      
    </li>
 
    <ul id="repos-container"></ul>
</ul> -->
<ul id="repos-container"></ul>
<style>

    * {
      box-sizing: border-box;
    }
    
    
    .cards {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin: 4rem 5vw;
      padding: 0;
      list-style-type: none;
    }
    
    .card {
      position: relative;
      display: block;
      height: 100%;  
      border-radius: calc(var(--curve) * 1px);
      overflow: hidden;
      text-decoration: none;
    }
    
    .card__image {      
      width: 100%;
      height: auto;
    }
    
    .card__overlay {
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      z-index: 1;      
      border-radius: calc(var(--curve) * 1px);    
      background-color: var(--mid-blue);      
      transform: translateY(100%);
      transition: .2s ease-in-out;
    }
    
    .card:hover .card__overlay {
      transform: translateY(0);
    }
    
    .card__header {
      position: relative;
      display: flex;
      align-items: center;
      gap: 2em;
      padding: 2em;
      border-radius: calc(var(--curve) * 1px) 0 0 0;    
      background-color: var(--mid-blue);
      transform: translateY(-100%);
      transition: .2s ease-in-out;
    }
    

    
    .card:hover .card__header {
      transform: translateY(0);
    }
    
    .card__thumb {
      flex-shrink: 0;
      width: 50px;
      height: 50px;      
      border-radius: 50%;      
    }
    
    .card__title {
      font-size: 1em;
      margin: 0 0 .3em;
      color: var(--beige-color);
    }
    
    /* .card__tagline {
      display: block;
      margin: 1em 0; 
      font-size: .8em; 
      color: var(--beige-color);  
    } */
    
    .card__status {
      font-size: .8em;
      color: var(--light-blue);
    }
    
    .card__description {
      padding: 0 2em 2em;
      margin: 0;
      color: var(--beige-color);
      font-family: "MockFlowFont";   
      display: -webkit-box;
      -webkit-box-orient: vertical;
      /* -webkit-line-clamp: 3; */
      overflow: hidden;
    }     
    </style>