<template>
  <div>
    <h1>v-text="aaaaaaaaaaa"</h1>
	<h3>mons (<span v-text="mons ? mons.length : 0" />)</h3>
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
			let arr: string[];
			return {
				mons: arr,
				loadingBox: false,
			};
		},

		mounted() {
			this.loadBox();
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
				this.mons = mon_arr;
				this.loadingBox = false;
			},
		},
	};
</script>