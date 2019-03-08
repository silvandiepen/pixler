<template>
	<main class="page page--home">
		<div class="row">
			<div class="column small-full medium-two-third canvas-column">
				<div :style="`--grid-size: ${size}`" class="pixel-canvas">
					<div
						v-for="(pixel, index) in canvas"
						:key="index"
						:class="['pixel-canvas__pixel', pixelColor(pixel)]"
						@click="setPixel(pixel)"
					></div>
				</div>
			</div>
			<div class="column small-full medium-third tools-column">
				<select v-model="size">
					<option value="8">8</option>
					<option value="12">12</option>
					<option value="16">16</option>
					<option value="24">24</option>
				</select>
				<ul class="colorset">
					<li
						v-for="(color, index) in colorset"
						:key="index"
						:class="['colorset__color', { 'colorset__color--current': color.id === currentColor }]"
						:style="`background-color: ${color.value}`"
						@click="setColor(color)"
					>
						{{ color.title }}
					</li>
				</ul>
			</div>
		</div>
	</main>
</template>

<script>
export default {
	data() {
		return {
			colorset: [
				{ title: 'black', id: 'b', value: '#000000' },
				{ title: 'white', id: 'w', value: '#ffffff' },
				{ title: 'red', id: 'r', value: '#ff0000' },
				{ title: 'orange', id: 'o', value: '#ff9900' },
				{ title: 'yellow', id: 'y', value: '#ffff00' },
				{ title: 'green', id: 'g', value: '#00cc00' },
				{ title: 'blue', id: 'a', value: '#6688ff' },
				{ title: 'purple', id: 'p', value: '#992299' }
			],
			size: 8,
			currentColor: null
		};
	},
	created() {
		this.canvas = this.createCanvas();
	},
	methods: {
		setPixel(pixel) {
			console.log('do something with this pixel', pixel, this.currentColor);
			pixel.color = this.currentColor;
		},
		pixelColor(pixel) {
			if (pixel.color !== null) {
				return `background--${pixel.color}`;
			} else {
				return '';
			}
		},
		setColor(color) {
			this.currentColor = color.id;
		},
		createCanvas() {
			let canvas = [];
			for (let i = 0; i < this.size * this.size; i++) {
				canvas.push({
					color: null
				});
			}
			return canvas;
		}
	}
};
</script>

<style lang="scss">
@import '~tools';

$colors: (
	'b': (
		'black',
		'#000000'
	),
	'w': (
		'white',
		'#ffffff'
	),
	'r': (
		'red',
		'#ff0000'
	),
	'o': (
		'orange',
		'#ff9900'
	),
	'y': (
		'yellow',
		'#ffff00'
	),
	'g': (
		'green',
		'#00cc00'
	),
	'a': (
		'blue',
		'#6688ff'
	),
	'p': (
		'purple',
		'#992299'
	)
);
.pixel-canvas {
	display: grid;
	grid-template-columns: repeat(var(--grid-size), 1fr);
	grid-template-rows: var(--grid-size);
	&__pixel {
		height: 0;
		padding-bottom: 100%;
		background-image: linear-gradient(to right bottom, color(Black, 0.1), color(Black, 0));
		@each $color in $colors {
			&.background--#{nth($color, 1)} {
				background-color: unquote(nth(nth($color, 2), 2));
			}
		}
	}
}
.colorset {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	&__color {
		height: 0;
		padding-bottom: 100%;
		transform: scale(0.85);
		border-radius: 4px;
		transition: transform 0.3s;
		text-indent: -999em;
		box-shadow: 0 0 10px 0 color(Black, 0.25);
		&--current {
			transform: scale(1);
		}
	}
}

.canvas-column {
	padding: grid(1);
}
.tools-column {
	padding: grid(1);
	background-color: color(Blue);
}

.intro {
	height: 100vh;
	width: 100vw;
	display: flex;
	align-items: center;
	justify-content: center;
}
</style>
