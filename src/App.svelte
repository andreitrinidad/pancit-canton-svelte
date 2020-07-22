<script>
	let activeColor = 'original'
	let shakeIt = false;

	const colors = [
		'original',
		'sweet',
		'calamansi',
		'spicy'	
	];

	function chooseAColor() {
		activeColor = colors[Math.floor(Math.random() * colors.length)];
	}

	function handleWucky() {
		shakeIt = true;

		setTimeout(() => {
			shakeIt = false;
		}, 1000)
	}
</script>

<svelte:head>
	<link href="https://fonts.googleapis.com/css2?family=Archivo+Black&display=swap" rel="stylesheet">
</svelte:head>

<main class={activeColor}>
	<div class="labels">
		<h2 on:click={handleWucky}>Wucky me!</h2>
		<h3>instant</h3>
		<h1>Cancit</h1>
		<h1>Panton</h1>
		<button class="flavor" on:click={chooseAColor}>{activeColor} flavor</button>
		<p>Net Wt: 69 grams <span>COOK IN 2 MINUTES</span></p>
		<div class="andrei">a site by <a href="https://fb.me/ughndrei" target="_blank">andreitrinidad</a></div>
	</div>

	<div class="pic {shakeIt && 'pic--animate'}">
		<img src="./cancit.png" alt="">
	</div>
</main>

<style type="text/scss">
	// variables
	$red: #af1e25;
	$yellow: #ffcd1b;
	$black: #111;
	$white: #fff;
	$green: #8bbf41;
	$tablet-width: 768px;
	$desktop-width: 1024px;

	:global(body), * {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	:global(body) {
		background-color: $black;
	}


	// breakpoints
	@mixin tablet {
		@media (min-width: #{$tablet-width}) and (max-width: #{$desktop-width - 1px}) {
			@content;
		}

		@media (min-width: #{$desktop-width}) {
			@content;
		}
	}

	@mixin desktop {
		@media (min-width: #{$desktop-width}) {
			@content;
		}
	}

	//animations
	@keyframes shake {
		0% { transform: translate(1px, 1px) rotate(0deg); }
		10% { transform: translate(-1px, -2px) rotate(-1deg); }
		20% { transform: translate(-3px, 0px) rotate(1deg); }
		30% { transform: translate(3px, 2px) rotate(0deg); }
		40% { transform: translate(1px, -1px) rotate(1deg); }
		50% { transform: translate(-1px, 2px) rotate(-1deg); }
		60% { transform: translate(-3px, 1px) rotate(0deg); }
		70% { transform: translate(3px, 1px) rotate(-1deg); }
		80% { transform: translate(-1px, -1px) rotate(1deg); }
		90% { transform: translate(1px, 2px) rotate(0deg); }
		100% { transform: translate(1px, -2px) rotate(-1deg); }
	}

	
	main {
		position: relative;
		display: flex;
		align-items: flex-start;
		justify-content: center;
		height: 100%;
		width: 100%;
		font-family: 'Archivo Black', sans-serif;
		padding: 0px 100px;
		overflow: hidden;

		@include desktop {
			align-items: center;
		}

		&:before {
			content: '';
			top: 0;
			left: 0;
			position: absolute;
			background: $black;
			width: 100%;
			height: 25px;

			@include tablet {
				width: 25px;
				height: 100%;

			}

			@include desktop {
				width: 50px;
				height: 100%;

			}
		}

		&:after {
			content: '';
			bottom: 0;
			right: 0;
			position: absolute;
			background: $black;
			width: 100%;
			height: 25px;
			z-index: 3;

			@include tablet {
				top: 0;
				bottom: unset;
				width: 25px;
				height: 100%;

			}

			@include desktop {
				width: 50px;
				height: 100%;

			}
		}


		.labels {
			margin-top: 50px;
			transform: scale(.75);
			// z-index: 2;
			
			@include tablet {
				transform: scale(1);
			}

			@include desktop {
				margin-top: unset;
				width: 1280px;
			}
			// big letters
			h1 {
				color: $black;
				font-size: 100px;
				text-transform: uppercase;
				font-size: 80px;
				line-height: 80px;
				

				&:first-of-type {
					font-size: 87px;
				}

				@include tablet {
					font-size: 100px;
					line-height: 100px;

					&:first-of-type {
						font-size: 107px;
					}
				}
			}

			// logo
			h2 {
				display: inline-block;
				font-style: italic;
				padding: 10px 20px;
				border-radius: 30px;
				color: $white;
				background-color: $red;
				border: 3px solid $white;
				margin-bottom: 20px;
				transition: transform 200ms ease-in-out;
				cursor: pointer;

				&:hover {
					transform: scale(1.05);
				}

				&:active {
					transform: scale(1);
				}

			}

			// instant text
			h3 {
				font-size: 24px;
				text-transform: uppercase;
				color: $black;
			}

			// flavor
			.flavor {
				display: inline-block;
				background-color: $black;
				color: $yellow;
				margin: 20px 0;
				padding: 10px 30px;
				text-transform: uppercase;
				border: none;
				border-radius: 20px;
				appearance: none;
				transition: transform 200ms ease-in-out;
				cursor: pointer;


				&:hover {
					transform: scale(1.05);
				}

				&:active {
					transform: scale(1);
				}

			}

			p {
				font-family: 'Franklin Gothic Medium', Arial, sans-serif;
				font-weight: normal;

				span {
					margin-left: 50px;
					color: $red;
					font-weight: bolder
				}
			}

			.andrei {
				position: relative;
				font-family: 'Courier New', Courier, monospace;
				font-weight: bold;
				margin-top: 50px;
				// background-color: salmon;

				> a {
					color: unset;
				}

				@include desktop {
					margin-top: 50px;
					// position: absolute;
					// bottom: 50px;
				}
	
			}
		}

		.pic {
			position: absolute;
			right: 0;
			bottom: -10px;
			width: 80vw;
			z-index: 1;

			@include tablet {
				width: 60vw;
			}

			@include desktop {
				width: 50vw;
				
			}

			img {
				width: 100%
			}

			&--animate {
				animation: shake 1s ease-in-out;
			}
		}

		&.original {
			background-color: $yellow;
			.flavor {
				color: $yellow;
			}
		}

		&.sweet {
			background-image: linear-gradient(to left, #e65d15, #efbf39);
			.flavor {
				color: #e65d15;
			}
		}

		&.calamansi {
			background-color: $green;
			.flavor {
				color: $green;
			}
		}
		&.spicy {
			background-image: linear-gradient(to left, #a3221d, #440a09);
			h1, h3, p, .andrei {
				color: $white;
			}

			.flavor {
				color: $white;
			}
		}
	}


	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
