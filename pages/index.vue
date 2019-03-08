<template>
	<main class="page page--home">
		<div class="row">
			<div class="column small-full medium-two-third">
				<div class="pixel-canvas">
					<divv-for="(pixel, index) in canvas" 
:key="index" :class="['pixel-canvas__pixel']" @click="setPixel"
>
						{{ canvas }}
					</div>
				</div>
			</div>
			<div class="column small-full medium-third">
				<ul class="colorset">
					<li
						v-for="(color, index) in colorset"
						:key="index"
						:class="['colorset__color', `background--${color}`]"
						@click="setColor"
					>
						{{ color }}
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
			colorset: ['black', 'white', 'red', 'orange', 'yellow', 'green', 'blue', 'purple'],
			canvas: []
		};
	},
	methods: {
		setPixel() {
			console.log('do something with this pixel');
			return;
		},
		setColor() {
			console.log('set the current color');
			return;
		}
	}
};
</script>

<style lang="scss">
@import '~tools';

.page {
	// general page styles
	&--home {
		// specific home styles
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
