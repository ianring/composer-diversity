<template lang="html">
	<div class="inputs">
		<header>
			<ul id="nav-menu">
				<li><a href="about.html">{{ $t("i18nKeys.abouttheproject")}}</a></li>
			</ul>
			<input type="text" v-model="query" class="search" v-bind:placeholder="$t('i18nKeys.search')" autofocus @input="updateSearch(query)" />
		</header>
		<div class="filters" id="filters" v-bind:class="{ collapsed: filtersCollapsed }">
			<div id="filters-heading">
				<a href="#" @click="toggleFilterView()">
					<h3><span class="icon">&#9660;</span> {{$t('i18nKeys.searchfilteroptions')}}</h3></a>
			</div>
			<div class="filter-section living-dead">
				<template v-if="filterOptions != null">
					<template v-for="option in filterOptions.slice(0,2)">
						<label class="filter" :class="vueFields[option].type">
							<input type="checkbox" value="X" v-model="filters[option]" @change="updateFilters(option)" />
							{{ $t( 'i18nKeys.' + vueFields[option].labelI18nKey ) }} 
							({{headings[option]}})
						</label>
					</template>
				</template>
			</div>
			<div class="filter-section gender">
				<template v-if="filterOptions != null">
					<template v-for="option in filterOptions.slice(2,4)">
						<label class="filter" :class="vueFields[option].type">
							<input type="checkbox" value="X" v-model="filters[option]" @change="updateFilters(option)" />
								<span :class="vueFields[option].type + ' badge'" @change="updateFilters(option)" >
									{{vueFields[option].icon}}
								</span>
								{{ $t( 'i18nKeys.' + vueFields[option].labelI18nKey ) }} 
								({{headings[option]}})
						</label>
					</template>
				</template>
			</div>
			<div class="filter-section genre">
				<h4><p>{{ $t("i18nKeys.genre") }}</p></h4>
				<template v-if="filterOptions != null">
					<template v-for="option in filterOptions.slice(startOfSection('genre')-2,startOfSection('genre') + numberOfType('genre')-2)">
						<label class="filter" :class="vueFields[option].type"><input type="checkbox" value="X" v-model="filters[option]" @change="updateFilters(option)" >
							<span :class="vueFields[option].type + ' badge'" @change="updateFilters(option)" >
								{{vueFields[option].icon}}
							</span>
							{{ $t( 'i18nKeys.' + vueFields[option].labelI18nKey ) }} 
							({{headings[option]}})
						</label>
					</template>
				</template>
			</div>
			<div class="filter-section medium">
				<h4>{{$t('i18nKeys.mediumsubgenre')}}</h4>
				<template v-if="filterOptions != null">
					<template v-for="option in filterOptions.slice(startOfSection('medium')-2,startOfSection('medium') + numberOfType('medium')-2)">
						<label class="filter" :class="vueFields[option].type"><input type="checkbox" value="X" v-model="filters[option]" @change="updateFilters(option)" >
							<span :class="vueFields[option].type + ' badge'" @change="updateFilters(option)" >
								{{vueFields[option].icon}}
							</span>
							{{ $t( 'i18nKeys.' + vueFields[option].labelI18nKey ) }} 
							({{headings[option]}})
						</label>
					</template>
				</template>
			</div>
			<div class="filter-section demographic">
				<h4>{{$t('i18nKeys.demographic')}}</h4>
				<template v-if="filterOptions != null">
					<template v-for="option in filterOptions.slice(startOfSection('demographic')-2,startOfSection('demographic') + numberOfType('demographic')-2)">
						<label v-if="vueFields[option].class != 'white'" class="filter" :class="vueFields[option].type">
							<input type="checkbox" value="X" v-model="filters[option]" @change="updateFilters(option)" >
							{{ $t( 'i18nKeys.' + vueFields[option].labelI18nKey ) }} 
							({{headings[option]}})
						</label>
					</template>
				</template>
			</div>
			<div class="filter-section location">
				<h4>{{$t('i18nKeys.location')}}</h4>
				<template v-if="filterOptions != null">
					<template v-for="option in filterOptions.slice(filterOptions.length-2)">
						<label class="filter" :class="option"><input type="checkbox" value="X" v-model="filters[option]" @change="updateFilters(option)" >
							{{ $t( 'i18nKeys.' + vueFields[option].labelI18nKey ) }} 
						</label>
					</template>
				</template>
			</div>
			<div class="filter-section clear-button" id="global-controls">
				<button @click="clearFilters()" class="clear-button">
					{{ $t('i18nKeys.clearallfilters') }}
				</button>
			</div>
			<div class="total">
				{{ $t('i18nKeys.composersmatchingfilters') }} {{filteredTotal}}
			</div>

		</div>
	</div>
</template>

<script>
export default {
	name: 'FormInputs',
	props: [
		'search',
		'filtersCollapsed',
		'filterOptions',
		'vueFields',
		'filters',
		'headings',
		'startOfSection',
		'numberOfType',
		'toggleFilterView',
		'filteredTotal'
	], // props
	data () {
		return {
			query: ''
		}
	},
	methods: {
		updateSearch: function(query) {
			this.$emit('updateSearch', {query})
			// console.log(query);
		}, // updateSearch
		updateFilters: function(option) {
			this.$emit('updateFilters', {option});
		}, // updateFilters
		clearFilters: function() {
			this.$emit('clearFilters')
		}, // updateFilters

	}
}
</script>

<style lang="css">
</style>
