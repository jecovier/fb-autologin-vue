# FB Auto Login for VUE 2
this component initialize the Facebook SDK and show the login pop up to the user.
It has a event when the user is login and three slots to show a different message
depending on the connection status.

## ✔ Getting started

Get the package:
```bash
npm install fb-autologin-vue
```

Register it in your app:
```js
import Vue from 'vue'
import FBAutologin from 'fb-autologin-vue';

Vue.component('fb-login', FBAutologin);
```

In your HTML call it like

```html
<fb-login
	@login = "login_callback">
	<template slot="check-login">
		connecting...
	</template>
	<template slot="cancelled">
		user cancelled the login
	</template>
	<template slot="logged">
		Welcome!
	</template>
</fb-login>
```


## License
MIT



#### Status
This project is in an early stage of development. Any contribution is welcome :D
