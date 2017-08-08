<style src="./sass/toast.scss" lang="scss"> </style>
<template>
    <div :id="containerId" :class="containerClasses">

        <div class="toasted" v-for="toast in toasts" :class="toastClasses(toast)">

            <span class="toasted--content" v-html="toast.message"></span>

            <template v-if="Array.isArray(toast.action)" v-for="action in toast.action">
                <a class="action"
                   :class="{ 'icon' : action.icon }"
                   v-if="typeof action == 'object'"
                   :href="action.href">
                    <i class="material-icons" v-if="action.icon" v-text="action.icon"></i>
                    {{ action.text }}
                </a>
            </template>

        </div>
    </div>
</template>
<script>
    export default {
    	name : 'vue-toasted',
        data(){
    		return {
    			containerId : 'toasted-container',
                options : {
    				// container
	                position : 'top-right',
	                duration : 500,
	                fullWidth : false,
	                fitToScreen : false,
	                containerClass : [],

	                // toast
	                className : null,
	                Icon : null,
	                theme : 'primary',
	                onComplete : null
                },
                toasts : [
                    {
	                    message : 'My Toast',
	                    icon : 'face',
	                    className : null,
                        action :[
	                        {
		                        text : 'Cancel',
		                        icon : 'check'
	                        }
                        ]
                    }
                ]
            }
        },
        computed : {
        	containerClasses(){
        		return [
        			this.options.position,
                    (this.options.fullWidth) ? 'full-width' : null,
                    (this.options.fitToScreen) ? 'fit-to-screen' : null,
                ]
            }
        },
        methods : {
        	toastClasses(toast){
		        let classes = [];

		        (toast.theme) ? classes.push(toast.theme) : classes.push(this.options.theme)

        		return classes
            }
        }
    }
</script>