<template>
	<div>
		<iframe width="100%" height="512" :src="'https://www.youtube.com/embed/'+ this.id + '?rel=0&amp;showinfo=0'" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
	</div>
</template>

<script>
export default {
	props:['id']
} 
</script>