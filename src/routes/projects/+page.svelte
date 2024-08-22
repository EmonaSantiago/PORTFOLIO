<script>
  import Card from "$lib/components/card.svelte";
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

<style>
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

