<template>
	<div class='edit_div' v-html="innerText" style="-webkit-user-select: auto" :contenteditable="canEdit" @focus="isLocked = true"
	 @blur="isLocked =
		false" @input="changeText">    </div>
</template>
<script>
	export default {
		name: 'editDiv',
		props: {
			value: {
				type: String,
				default: ''
			},
			canEdit: {
				type: Boolean,
				default: true
			}
		},
		data() {
			return {
				innerText: this.value,
				isLocked: false
			}
		},
		watch: {
			'value'() {
				if (!this.isLocked ||
					!this.innerText) {
					this.innerText = this.value;
				}
			}
		},
		methods: {
			changeText() {
				this.$emit('input', this.$el.innerHTML);
			}
		}
	}
</script>   <style>
	.edit_div {
		outline: 0;
		font-size: 26upx;
	}

	.edit-div {
		width: 100%;
		height: 100%;
		overflow: auto;
		word-break: break-all;
		outline: none;
		user-select: text;
		white-space: pre-wrap;
		text-align: left;

		&[contenteditable=true] {
			user-modify:
				read-write-plaintext-only;

			&:empty:before {
				content: attr(placeholder);
				display: block;
				color: #ccc;
			}
		}
	}
</style>
