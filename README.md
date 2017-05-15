# FB Auto Login for VUE 2
this component initialize FB SDK and show the login pop up.

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
	<template slot="not-login">
		you are not login
	</template>
</fb-login>
```


## License
MIT



#### Status
This project is in an early stage of development. Any contribution is welcome :D
