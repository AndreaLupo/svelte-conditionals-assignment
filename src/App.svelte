<script>
	let password = '';
	let passwords = [];
	$: tooShort = password.length < 5;
	$: tooLong = password.length > 10;
	function addPassword() {
		if(tooShort || tooLong) {
			return;
		} 

		passwords = [...passwords, password];
	}

	function removePassword(currentIndex) {
		// remove one element
		console.log('Remove the element at index', currentIndex);
		passwords = passwords.filter((password, index) => {return index !== currentIndex;});
	}

</script>



<h1>Assignment</h1>

<p>Solve these tasks.</p>

<ol>
	<li>Add a password input field and save the user input in a variable.</li>
	<li>Output "Too short" if the password is shorter than 5 characters and "Too long" if it's longer than 10.</li>
	<li>Output the password in a paragraph tag if it's between these boundaries.</li>
	<li>Add a button and let the user add the passwords to an array.</li>
	<li>Output the array values (= passwords) in a unordered list (ul tag).</li>
	<li>Bonus: If a password is clicked, remove it from the list.</li>
</ol>

<input type="password" bind:value={password} />
<button on:click="{addPassword}">Add password</button>

{#if tooShort}
	<p>Password too shorrt</p>
{:else if tooLong}
	<p>Password too long</p>
{:else}
	<p>Last password inserted: {password}</p>
{/if}

<h1>Password list</h1>

<ul>
	{#each passwords as currentPwd, currentIndex}
	<li class="remove" on:click="{() => removePassword(currentIndex)}">{currentPwd}</li>
	{:else}
		<p>Input some passwords.</p>
	{/each}
</ul>


<style>
.remove {
	cursor: pointer;
}
</style>