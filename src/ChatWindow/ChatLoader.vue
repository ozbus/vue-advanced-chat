<template>
	<transition name="fade-spinner" appear>
		<div class="container-center" v-if="show">
			<div id="circle"></div>
		</div>
	</transition>
</template>

<script>
export default {
	name: 'chat-loader',
	props: ['show']
}
</script>

<style lang="scss" scoped>
.container-center {
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%, -50%);
	z-index: 9999;
}

#circle {
	height: 32px;
	width: 32px;
	border: 3px rgba(0, 0, 0, 0.25) solid;
	border-top: 3px var(--chat-color-spinner) solid;
	border-right: 3px var(--chat-color-spinner) solid;
	border-bottom: 3px var(--chat-color-spinner) solid;
	border-radius: 50%;
	-webkit-animation: spin 1s infinite linear;
	animation: spin 1s infinite linear;
}

@-webkit-keyframes spin {
	from {
		-webkit-transform: rotate(0deg);
		transform: rotate(0deg);
	}
	to {
		-webkit-transform: rotate(359deg);
		transform: rotate(359deg);
	}
}
@keyframes spin {
	from {
		-webkit-transform: rotate(0deg);
		transform: rotate(0deg);
		-webkit-transform: rotate(0deg);
		transform: rotate(0deg);
	}
	to {
		-webkit-transform: rotate(359deg);
		transform: rotate(359deg);
		-webkit-transform: rotate(359deg);
		transform: rotate(359deg);
	}
}
</style>
