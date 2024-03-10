<template>
  <div>
    <h1 v-text="raw" />
	<h3 v-text="mons" />
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>

<script lang="ts" type="module">
	export default {
		data() {
			let arr: string[] = [];
			return {
				raw: "",
				mons: arr,
				loadingBox: false,
			};
		},

		async mounted() {
			await this.loadBox();
		},
		methods: {
			async loadBox() {
				this.loadingBox = true;
				const resp = await fetch("https://rebornwebserver.pages.dev/box/");
				let mon_arr: string[] = [];
				const mons = await resp.json();
				for (let mon in mons) {
					mon_arr.push(mon);
				}
				this.raw = mons;
				this.mons = mon_arr;
				this.loadingBox = false;
			},
		},
	};
</script>