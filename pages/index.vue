<template>
	<main class="page page--home">
		<div class="row">
			<div class="column small-full medium-two-third canvas-column">
				<div :style="`--grid-size: ${size}`" class="pixel-canvas">
					<div
						v-for="(pixel, index) in canvas"
						:key="index"
						:class="['pixel-canvas__pixel', pixelColor(pixel)]"
						@click="setPixel(index)"
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
				{ title: 'black', id: 'a', value: '#000000' },
				{ title: 'white', id: 'b', value: '#ffffff' },
				{ title: 'red', id: 'c', value: '#ff0000' },
				{ title: 'orange', id: 'd', value: '#ff9900' },
				{ title: 'yellow', id: 'e', value: '#ffff00' },
				{ title: 'green', id: 'f', value: '#00cc00' },
				{ title: 'blue', id: 'g', value: '#6688ff' },
				{ title: 'purple', id: 'h', value: '#992299' }
			],
			size: 8,
			currentColor: null,
			canvas: []
		};
	},
	watch: {
		size: {
			handler() {
				this.canvas = this.createCanvas();
			}
		}
	},
	created() {
		this.canvas = this.createCanvas();
	},
	methods: {
		setPixel(index) {
			this.canvas[index].color = this.currentColor;
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
	'a': (
		'black',
		'#000000'
	),
	'b': (
		'white',
		'#ffffff'
	),
	'c': (
		'red',
		'#ff0000'
	),
	'd': (
		'orange',
		'#ff9900'
	),
	'e': (
		'yellow',
		'#ffff00'
	),
	'f': (
		'green',
		'#00cc00'
	),
	'g': (
		'blue',
		'#6688ff'
	),
	'h': (
		'purple',
		'#992299'
	)
);
.pixel-canvas {
	display: grid;
	grid-template-columns: repeat(var(--grid-size), 1fr);
	grid-template-rows: var(--grid-size);
	grid-gap: 4px;
	padding: 4px;
	box-shadow: 0 0 1rem 0 color(Black, 0.25);
	border-radius: 4px;
	&__pixel {
		height: 0;
		padding-bottom: 100%;
		background-image: linear-gradient(to right bottom, color(Black, 0.05), color(Black, 0));
		border-radius: 2px;
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
	background-color: color(Offwhite);
	padding: grid(1);
	@media #{$medium-up} {
		height: 100vh;
	}
}
.tools-column {
	padding: grid(1);
	background-color: color(Dark);
	@media #{$medium-up} {
		height: 100vh;
	}
}

.intro {
	height: 100vh;
	width: 100vw;
	display: flex;
	align-items: center;
	justify-content: center;
}
</style>
