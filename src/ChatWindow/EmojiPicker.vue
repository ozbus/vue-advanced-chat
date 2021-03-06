<template>
	<div class="wrapper">
		<emoji-picker @emoji="append" :search="search">
			<div
				class="svg-button"
				slot="emoji-invoker"
				slot-scope="{ events: { click: clickEvent } }"
				@click.stop="clickEvent"
				@click="openEmoji"
			>
				<svg-icon name="emoji" />
			</div>
			<div
				slot="emoji-picker"
				slot-scope="{ emojis, insert }"
				v-if="emojiOpened"
			>
				<div class="emoji-picker">
					<div class="emoji-picker__search">
						<input type="text" v-model="search" v-focus />
					</div>
					<div>
						<div v-for="(emojiGroup, category) in emojis" :key="category">
							<h5 v-if="category !== 'Frequently used'">{{ category }}</h5>
							<div class="emojis" v-if="category !== 'Frequently used'">
								<span
									v-for="(emoji, emojiName) in emojiGroup"
									:key="emojiName"
									@click="insert(emoji)"
									:title="emojiName"
									>{{ emoji }}</span
								>
							</div>
						</div>
					</div>
				</div>
			</div>
		</emoji-picker>
	</div>
</template>

<script>
import EmojiPicker from 'vue-emoji-picker'
import SvgIcon from './SvgIcon'

export default {
	components: {
		EmojiPicker,
		SvgIcon
	},
	props: ['emojiOpened'],
	data() {
		return {
			search: ''
		}
	},
	methods: {
		append(emoji) {
			this.$emit('addEmoji', emoji)
		},
		openEmoji() {
			this.$emit('openEmoji', true)
		}
	},
	directives: {
		focus: {
			inserted(el) {
				el.focus()
			}
		}
	}
}
</script>

<style scoped>
.wrapper {
	position: relative;
	display: flex;
}

.regular-input {
	padding: 0.5rem 1rem;
	border-radius: 3px;
	border: var(--chat-border-style);
	width: 20rem;
	height: 12rem;
	outline: none;
}

.emoji-picker {
	position: absolute;
	bottom: 32px;
	right: 10px;
	border: var(--chat-border-style);
	width: 15rem;
	height: 20rem;
	overflow: scroll;
	padding: 1rem;
	box-sizing: border-box;
	border-radius: 0.5rem;
	background: var(--chat-emoji-bg-color);
}

.emoji-picker__search {
	display: flex;
}

.emoji-picker__search > input {
	flex: 1;
	border-radius: 10rem;
	border: var(--chat-border-style);
	padding: 0.5rem 1rem;
	outline: none;
	background: var(--chat-bg-color-input);
	color: var(--chat-color);
}

.emoji-picker h5 {
	margin-bottom: 0;
	color: #b1b1b1;
	text-transform: uppercase;
	font-size: 0.8rem;
	cursor: default;
}

.emoji-picker .emojis {
	display: flex;
	flex-wrap: wrap;
	justify-content: space-between;
}

.emoji-picker .emojis:after {
	content: '';
	flex: auto;
}

.emoji-picker .emojis span {
	padding: 0.2rem;
	cursor: pointer;
	border-radius: 5px;
}

.emoji-picker .emojis span:hover {
	background: var(--chat-sidemenu-bg-color-hover);
	cursor: pointer;
}
</style>
