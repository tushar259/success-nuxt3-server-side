<template>
  <div>
    <!-- <NuxtWelcome /> -->
	<div v-for="industry in allIndustry">
		{{industry.which_industry}}
	</div>
  </div>
</template>

<script>
	export default{
		// data: () => ({
		// 	apiUrl: null,
		// 	allIndustry: [],
		// }),

		async setup() {
			const allIndustry = ref([]);
			// this.apiUrl = this.$axios.defaults.baseURL;

			
			const response = await useFetch(`http://127.0.0.1:8000/api/get-list-of-industries`)
			
			if(response.data.value.success === true){
				allIndustry.value = response.data.value.all_industry;
			}
			else{
				allIndustry.value = [];
			}
			
			console.log("response: ",response.data.value.success);
			return {
				allIndustry,
			};
		},

		created(){
			console.log("allIndustry: ", this.allIndustry);
		}
		
	}
</script>
