<template>
  <div class="modal fade show" @click.self="closeModal">
        <div class="modal-dialog">
            <div class="modal-content" :class="{'bg-red': theme === 'contact'}">
                <div class="modal-header">
                    <slot name="header"></slot>
                </div>
                <div class="modal-body">
					<slot/>
                </div>
                <div class="modal-footer">
					<slot name="footer"></slot>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        title:{
            type:String,
            required :true,
        },
        content:{
            type:String,
            default:"Body",
            required:false,
        },
        theme:{
			type:String,
			default:"example",
			validator (val){
				return	["example","sales","contact"].includes(val);
			},
		}
    },
    methods: {
        closeModal(){
            this.$emit('closeModal');
        }
    },


}
</script>

<style scoped lang="css">
	.modal {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1060;
    display: block;
    width: 100%;
    height: 100%;
    overflow-x: hidden;
    overflow-y: auto;
    outline: 0;
		background-color: rgba(0,0,0,.2);
	}
	.fade {
    transition: opacity .15s linear;
}
.modal-dialog {
    width: 500px;
    position: absolute;
		left: 35%;
		top: 80px;
		transform: translateX(-35%);
    margin: 0.5rem;
    pointer-events: none;
		
}
.modal.fade .modal-dialog {
    transition: transform .3s ease-out;
    transform: translate(0,-50px);
}
.modal-content {
    position: relative;
    display: flex;
    flex-direction: column;
    width: 100%;
    pointer-events: auto;
    background-color: #fff;
    background-clip: padding-box;
    border: 1px solid rgba(0,0,0,.2);
    border-radius: 0.3rem;
    outline: 0;
    text-align: center;
}
.modal-header {
    display: flex;
    flex-shrink: 0;
    align-items: center;
    justify-content: center;
    padding: 1rem 1rem;
    border-bottom: 1px solid #dee2e6;
    border-top-left-radius: calc(0.3rem - 1px);
    border-top-right-radius: calc(0.3rem - 1px);
}
.modal-body {
    position: relative;
    flex: 1 1 auto;
    padding: 1rem;
}
.modal-footer {
    display: flex;
    flex-wrap: wrap;
    flex-shrink: 0;
    align-items: center;
    justify-content: center;
    padding: 0.75rem;
    border-top: 1px solid #dee2e6;
    border-bottom-right-radius: calc(0.3rem - 1px);
    border-bottom-left-radius: calc(0.3rem - 1px);
}
.bg-red{
	background-color: red;
}
</style>