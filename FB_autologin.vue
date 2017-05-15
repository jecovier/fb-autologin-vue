<template>
	<div v-if=" logged == 'cancelled'">
		<slot
			name="cancelled">
		</slot>
		<button
			@click = "login"
			type   = "button"
			class  = "btn btn-primary">
			Facebook Login
		</button>
	</div>
	<div v-else-if=" logged == 'not_logged'">
		<slot
			name="check-login">
			Connecting with facebook...
		</slot>
	</div>
	<div v-else-if=" logged == 'logged'">
		<slot
			name="logged">
			Welcome!
		</slot>
	</div>
</template>



<script>
	export default {
		data: function() {
			return {
				logged: 'not_logged'
			};
		},
		props: {
			'appid':{
				type: String,
				required: true
			},
			'version':{
				type: String,
				default: 'v2.9',
			}
		},
		created(){
			var app = this;
			window.fbAsyncInit = ()=>{
				FB.init({
					appId   : app.appid,
					xfbml   : true,
					version : app.version
				});
				FB.AppEvents.logPageView();
				FB.getLoginStatus(app.check_login);
			};

			(function(d, s, id) {
				var js, fjs = d.getElementsByTagName(s)[0];
				if (d.getElementById(id)) {
					return;
				}
				js     = d.createElement(s);
				js.id  = id;
				js.src = "//connect.facebook.net/en_US/sdk.js";
				fjs.parentNode.insertBefore(js, fjs);
			}(document, 'script', 'facebook-jssdk'));
		},
		methods: {
			cancelled: function(response) {
				//FB.login(this.check_login);
				this.logged = 'cancelled';
			},
			logged_in: function() {
				this.logged = 'logged';
				this.$emit('logged');
			},
			login: function(){
				FB.login(this.check_login);
			},
			check_login: function(response){
				if (response.status === 'connected') {
					this.logged_in(response)
				}
				else {
					FB.login((response)=>{
						if (response.status === 'connected') {
							this.logged_in(response)
							return;
						}

						this.cancelled(response)
					});
				}
			}//end check_login
		}
	}
</script>
