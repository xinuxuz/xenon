<template>
	<div class="theme-options">
		<div v-if="xenon.extraOptions && xenon.extraOptions.above" class="user-options-above">
			<component :is="xenon.extraOptions.above" />
		</div>
		<ul v-if="xenon.hasThemes" class="color-theme-options">
			<li>
				<a href="#" class="default-theme" @click.prevent="setTheme()"></a>
			</li>
			<li v-for="color in xenon.themes" :key="color">
				<a href="#" :class="`${color}-theme`" @click.prevent="setTheme(color)"></a>
			</li>
		</ul>
		<div v-if="!xenon.disableDarkTheme" class="dark-theme-options toggle-option">
			<label for="dark-theme-toggle">Tungi ko'rinish</label>
			<input id="dark-theme-toggle" v-model="darkTheme" type="checkbox" @change="toggleDarkTheme" />
		</div>
		<div v-if="xenon.hasThemes && !xenon.disableThemeIgnore" class="force-theme-options toggle-option">
			<label for="force-theme-toggle">Avtomatik ko'rinish</label>
			<input id="force-theme-toggle" v-model="ignoreForcedThemes" type="checkbox" @change="toggleForcedThemes" />
		</div>
		<div v-if="xenon.extraOptions && xenon.extraOptions.below" class="user-options-below">
			<component :is="xenon.extraOptions.below" />
		</div>
	</div>
</template>

<script>
import xenonConfig from '@theme/mixins/xenonConfig.js';
import themeHandler from '@theme/mixins/themeHandler.js';
import darkThemeHandler from '@theme/mixins/darkThemeHandler.js';

export default {
	name: 'ThemeOptions',
	mixins: [xenonConfig, themeHandler, darkThemeHandler],
};
</script>

<style lang="stylus">
@import '../../styles/variables.styl';

.color-theme-options {
	display: flex;
	justify-content: space-around;

	li {
		width: 33%;
		text-align: center;

		a {
			width: 15px;
			height: 15px;
			border-radius: 2px;

			&.default-theme {
				background-color: $accentColor;
			}

			&.blue-theme {
				background-color: $blueAccentColor;
			}

			&.red-theme {
				background-color: $redAccentColor;
			}

			&.purple-theme {
				background-color: $purpleAccentColor;
			}
		}
	}
}

.toggle-option {
	display: flex;
	justify-content: space-between;
	align-items: center;

	label {
		padding-right: 0.25em;
	}
}
</style>
