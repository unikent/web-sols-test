<template>
	<div id="app">
		<headerPanel></headerPanel>
		<main>
			<div class="panel panel--content panel--heading kar-panel first">
				<div class="panel__body">
					<div class="content content--main content--profile">
						<section id="publications" class="kar">
							<h2 class="kar__title">Publications</h2>
							<div class="kar__body">
								<ul class="KARpublications">
								<template v-for="publication in publications">
									<karItem :data="publication" :key="publication.id"></karItem>
								</template>
								</ul>
								<div class="KARfooter">
									<p>Information obtained from the <a href="http://kar.kent.ac.uk/" class="KARExternal">Kent Academic Repository</a>, University of Kent's official repository of academic activity. <a href="https://www.kent.ac.uk/library/research/kar/" class="KARExternal">Find out more about the Kent Academic Repository</a>.</p>
									<p><a href="https://kar.kent.ac.uk/cgi/search/advanced?keywords=cequfin" class="KARExternal">View all publications listed above in the Kent Academic Repository</a>.</p>
								</div>
							</div>
						</section>
					</div>
				</div>
			</div>
		</main>
	</div>
</template>

<script>
import headerPanel from '@/templates/header-panel';
import karItem from '@/templates/kar-item';

export default {
    name: 'developer-test',
    components: {
		headerPanel,
        karItem
    },
    data() {
        return {
			publications: null
        }
    },
    methods: {
		get_data() {
			fetch('https://api.kent.ac.uk/api/v1/kar/keyword/cequfin/APA/all?offset=01&limit=25')
				.then(response => {
					if (!response.ok) {
						throw new Error("HTTP error " + response.status);
					}
					return response.json();
				})
				.then((data) => {
					// Work with JSON data here
					this.publications = data.publications;
				})
				.catch((err) => {
					// Do something for an error here
					console.error(err)
				})
		}
	},
	created() {
		this.get_data();
	}
}
</script>

<style>
.KARitem {
    margin-bottom: 1em;
	font-size: .9rem;
}
.KARlinks {
	margin: .25em 0 0 1.5em;
}
.KARlink {
    margin-right: 1%;
}
.abstractIcon {
    margin-left: 5px;
    border: solid #000;
    border-width: 0 3px 3px 0;
    display: inline-block;
	padding: 3px;
}
.down {
    transform: rotate(45deg);
    -webkit-transform: rotate(45deg);
	margin-bottom: 3%;
}
.KARlinks > p {
    border-left: 2px solid #05345c;
    padding-left: 1em;
	margin-top: 1%;
}
.KARfooter {
	margin-bottom: 5rem;
    padding-top: 1rem;
	border-top: 1px solid #e6e6e6;
	font-size: .8rem;
}
</style>