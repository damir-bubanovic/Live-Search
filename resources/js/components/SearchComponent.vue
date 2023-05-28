<template>
	<div class="card">
			<div class="card-header text-center fs-1 bg-info text-white fw-bolder">Search Available Books</div>

			<div class="card-body">
				<div class="input-group input-group-lg mb-4 mt-2">
				  <input type="text" v-model="keyword" placeholder="Search by Keyword" class="form-control bg-info-subtle" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-lg">
				</div>
				<ol class="list-group list-group-numbered">
					 <li class="list-group-item" v-for="book in books">{{ book.title }}</li> 
				</ol>
			</div>
	</div>
</template>

<script>
export default {
	data() {
			return {
					books: [],
					keyword: null,
			};
	},
	mounted() {
			this.list();
	},
	watch: {
			keyword(after, before) {
					this.search();
			}
	},
	methods: {
			list() {
					var self = this;

					axios.get('/list')
							.then(function(response) {
									self.books = response.data;
							})
			},
			search() {
					var self = this;

					const data = { keyword: self.keyword }

					axios.post('/search', data)
							.then(function(response) {
									self.books = response.data;
							});
			}
	}
}
</script>
