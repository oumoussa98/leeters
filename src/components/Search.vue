<template>
	<div class="search">
		<div class="input">
			<span class="search-icon">
				<SearchIcon />
			</span>
			<input
				ref="searchInput"
				id="search"
				placeholder="Search (press / to focus)"
				v-model="searchTerm"
				type="search"
			/>
		</div>
		<div v-if="searchTerm" class="results">
			<div v-if="!results.length">
				<div class="title">No matching results :(</div>
			</div>
			<div v-else class="list" v-for="(result, i) in results" :key="i" @click="clear">
				<g-link class="link" :to="result.path">
					<div class="title">{{ result.title }}</div>
					<div class="desc">
						{{ description(result.description) }}
					</div>
					<div class="date">
						{{ result.date }}
					</div>
				</g-link>
			</div>
		</div>
	</div>
</template>
<static-query>
query {
  posts: allPost{
    edges {
      node {
        id
        title
        description
		date (format: "MMMM D, YYYY")
        path
      }
    }
  }
}
</static-query>
<script>
import Flexsearch from "flexsearch";
import SearchIcon from "~/components/svg/SearchIcon";
export default {
	components: { SearchIcon },
	data() {
		return {
			results: [],
			index: null,
			searchTerm: "",
		};
	},
	watch: {
		searchTerm: function(newValue, oldValue) {
			this.searchResults();
		},
	},
	methods: {
		searchResults() {
			if (this.index === null || this.searchTerm.length < 3) this.results = null;
			this.results = this.index.search({
				query: this.searchTerm,
				limit: 10,
			});
		},
		clear() {
			this.searchTerm = "";
		},
		description: desc =>
			desc
				.split(" ")
				.splice(0, 13)
				.join(" ") + "...",
	},
	beforeMount() {
		this.index = new Flexsearch({
			tokenize: "forward",
			doc: {
				id: "id",
				field: ["title", "description", "date"],
			},
		});
		this.index.add(this.$static.posts.edges.map(e => e.node));
	},
	mounted() {
		window.onclick = e => {
			if (e.target == this.$refs.searchInput) return;
			else this.clear();
		};
		document.addEventListener("keypress", e => {
			if (e.key === "/") {
				document.querySelector("#search").focus();
				e.preventDefault();
			} else return;
		});
	},
};
</script>

<style scoped>
.search {
	position: relative;
	margin-left: 10px;
}
.search .search-icon {
	position: absolute;
	bottom: 2px;
	left: 8px;
}
.search input {
	height: 36px;
	width: 400px;
	padding: 0 10px 0 30px;
	border: 2px solid var(--border-color);
	color: var(--body-color);
	outline: none;
	border-radius: 14px;
	transition: background 0.6s, border-color 0.5s ease;
	background: var(--bg-color);
	font-size: 1em;
	font-weight: 300;
}
.search input:focus {
	border-color: var(--link-color);
}
.results {
	position: absolute;
	display: block;
	width: 400px;
	max-height: 80vh;
	padding: 10px 5px;
	left: 0px;
	top: 37px;
	overflow: auto;
	background-color: var(--bg-content-color);
	border-radius: 5px;
	text-align: center;
	box-shadow: 0px 3px 4px rgba(0, 0, 0, 0.2);
	z-index: 99;
	font-size: 0.8rem;
}
.link {
	margin-top: 10px;
}
.results .list {
	padding: 6px;
	border-bottom: 1px solid var(--bg-color);
}
.results .list a {
	display: block;
}
.results .list:hover {
	background: var(--search-hover-color);
	border-radius: 4px;
}
.title {
	width: 100%;
	font-size: 18px;
	line-height: 1.2;
	margin-bottom: 5px;
	color: var(--search-results-color);
}
.desc {
	color: var(--body-color);
	width: 100%;
}
.date {
	color: var(--link-color);
	opacity: 0.6;
	font-weight: 100;
	width: 140px;
	margin: 6px auto 0 auto;
}
.link {
	display: flex;
	text-decoration: none;
	justify-content: center;
}
@media only screen and (max-width: 600px) {
	.search input {
		width: 60vw;
		font-size: 1.1em;
	}
	.results {
		width: 60vw;
	}
}
@media only screen and (max-width: 500px) {
	.search input {
		font-size: 1em;
	}
	.menu {
		font-size: 30px;
		margin-top: 6px;
		margin-right: 8px;
	}
}
</style>