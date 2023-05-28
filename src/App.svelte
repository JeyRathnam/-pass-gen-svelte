<script>
	export let password;
	let includeSymbols = true;
	let showPassword = true;
	const alphaNumeric = `abcdefghijklmonpqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789`;
	const keyboardSymbols = `!@#$%^&*()-=_+[]{}|;:'",.<>/?`;
	let length = 30;
	let toast;

	function generatePassword(len = 10) {
		let inputString = alphaNumeric;
		let password = '';
		if (includeSymbols) {
			inputString += keyboardSymbols;
		}

		for (let i = 0; i < len; i++) {
			password += inputString[Math.floor(Math.random() * inputString.length)]
		}

		return password;
	}

	function maskPassword(password) {
		const maskCharacter = '*';
		let maskedPassword = '';

		for (let i=0; i<password.length; i++) {
			maskedPassword += maskCharacter;
		}
		return maskedPassword;
	}

	function copyToClipboard() {
		navigator.clipboard.writeText(password).then(() => {
			console.log(toast)

		toast.classList.add("show");
		toast.style.visibility = "visible";
		
		setTimeout(function(){

			toast.classList.remove("show");
			toast.style.visibility = "hidden";
		}, 3000);
		})
	}

	password = generatePassword(length);


</script>

<main>
	<div class="header">Free Password Generator</div>
	<div class="password">
	<h1>{showPassword ? password : maskPassword(password)}</h1>
	<div class="controls">
		<div on:click={() => copyToClipboard()} on:keypress={() => copyToClipboard()}>
	<svg xmlns="http://www.w3.org/2000/svg" width="200"  fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6" >
		<path stroke-linecap="round" stroke-linejoin="round" d="M8.25 7.5V6.108c0-1.135.845-2.098 1.976-2.192.373-.03.748-.057 1.123-.08M15.75 18H18a2.25 2.25 0 002.25-2.25V6.108c0-1.135-.845-2.098-1.976-2.192a48.424 48.424 0 00-1.123-.08M15.75 18.75v-1.875a3.375 3.375 0 00-3.375-3.375h-1.5a1.125 1.125 0 01-1.125-1.125v-1.5A3.375 3.375 0 006.375 7.5H5.25m11.9-3.664A2.251 2.251 0 0015 2.25h-1.5a2.251 2.251 0 00-2.15 1.586m5.8 0c.065.21.1.433.1.664v.75h-6V4.5c0-.231.035-.454.1-.664M6.75 7.5H4.875c-.621 0-1.125.504-1.125 1.125v12c0 .621.504 1.125 1.125 1.125h9.75c.621 0 1.125-.504 1.125-1.125V16.5a9 9 0 00-9-9z" />
	  </svg>
	</div>
	<div on:click={() => password = generatePassword(length)} on:keypress={() => password = generatePassword(length)}>
	  <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
		<path stroke-linecap="round" stroke-linejoin="round" d="M16.023 9.348h4.992v-.001M2.985 19.644v-4.992m0 0h4.992m-4.993 0l3.181 3.183a8.25 8.25 0 0013.803-3.7M4.031 9.865a8.25 8.25 0 0113.803-3.7l3.181 3.182m0-4.991v4.99" />
	  </svg>
	  </div>
	</div>
</div>
	<div class="includeSymbolsContainer">
<label>
	<input type="checkbox" bind:checked={includeSymbols} on:change={() => password = generatePassword(length)}/>
	Include symbols?
</label>
</div>

<div class="showPasswordContainer">
	<label>
		<input type="checkbox" bind:checked={showPassword} />
		
		Show password?
	</label>
	</div>

<div class="slidercontainer">
	<label>
	<input type="range" min="1" max="30" value={length} class="slider" id="myRange" on:input={(e) => {length = e.target.value; password = generatePassword(length)}}>
	<span class="slider-value">{length}</span></label>
  </div>

  <div  bind:this={toast} id="toast" class="toast">Copied</div>
</main>

<style>
	main {
		height: 100%;
		text-align: center;
		margin: 0 auto;
	}

	div {
		margin-bottom: 10px;
	}

	.header {
		display: flex;
		text-align: center;
		justify-content: center;
		font-weight: 600;
		font-size: 20px;
		background-color: #e2702b;
		color: white;
		height: 30px;
	}

	h1 {
		color: #ff3e00;
		font-size: 4vw;
		font-weight: 100;	
	}

	.controls {
		display : flex;
		gap: 1em;
	}

	.password {
		display: flex;
		flex-direction: column;
		text-align: center;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	.password h1 {
		margin: 0.2em;
		text-align: center;
		padding-right: .5em;
	}

	.password div svg {
		width: 2em;
	}

	.toast {
      visibility: hidden;
      min-width: 250px;
      margin-left: -125px;
      text-align: center;
      border-radius: 2px;
      padding: 16px;
      position: fixed;
      z-index: 1;
      left: 50%;
      bottom: 30px;
      font-size: 17px;
    }
    .toast .show {
      /* visibility: visible; */
      -webkit-animation: fadein 0.5s, fadeout 0.5s 2.5s;
      animation: fadein 0.5s, fadeout 0.5s 2.5s;
    }
    @-webkit-keyframes fadein {
      from {bottom: 0; opacity: 0;}
      to {bottom: 30px; opacity: 1;}
    }
    @keyframes fadein {
      from {bottom: 0; opacity: 0;}
      to {bottom: 30px; opacity: 1;}
    }
    @-webkit-keyframes fadeout {
      from {bottom: 30px; opacity: 1;}
      to {bottom: 0; opacity: 0;}
    }
    @keyframes fadeout {
      from {bottom: 30px; opacity: 1;}
      to {bottom: 0; opacity: 0;}
    }

	.slidercontainer {
  position: relative;
}

.slider {
  -webkit-appearance: none;
  appearance: none;
  width: 30vw;
  height: 5px;
  background-color: #e4dddd;
  outline: none;
  opacity: 1;
  transition: opacity 0.2s;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 20px;
  height: 20px;
  background-color: #e2702b;
  cursor: pointer;
  border-radius: 4px;
  border-color: transparent;
}

.slider::-moz-range-thumb {
  width: 15px;
  height: 25px;
  background-color: #e2702b;
  cursor: pointer;
  border-radius: 4px;
  border-color: transparent;
}

.slider-value {
  position: absolute;
  top: 25px;
  left: 0;
  width: 100%;
  text-align: center;
}



	

	@media (max-width: 992px) {
		.password {
		display: flex;
	}

		main {
			max-width: none;
		}

		h1 {
		color: #ff3e00;
		font-size: 5vw;
		font-weight: 600;
	}

	.password div svg {
		width: 4em;
	}

	.slider {
		width: 50vw;
		height: 2px;
	}

	.slider::-webkit-slider-thumb  { 
		width: 15px;
		height: 30px;
	}

	.slider::-moz-range-thumb {
		width: 15px;
		height: 30px;
	}
	}


	@media (prefers-color-scheme: white) {
		main {
			background-color: #25013f;
		}
		
		h1 {
		color: #f0eeee;
		}

		svg {
			stroke: white;
		}

		label {
			color: white;
		}

		.toast {
			color: white;
		}

		.slider {
			background-color: #e9e9e9;
			
		}
	}
</style>