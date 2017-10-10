<template>
	<div>
		<div class="header">
			<div class="content-wrapper">
				<div class="avatar">
					<img :src="seller.avatar" width="64" height="64">
				</div>
				<div class="content">
					<span class="brand"></span>
					<div class="title">{{seller.name}}</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
  export default {
    props: {
      seller: {
        type: Object
      }
    }
  }
</script>

<style>
	
</style>