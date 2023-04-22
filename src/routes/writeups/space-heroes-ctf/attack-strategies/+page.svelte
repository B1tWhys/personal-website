<script>
	import emptyForm from './empty_form.png';
	import filledInForm from './filled_in_form.png';
	import normalRequest from './normal_request.png';
	import editAndResend from './edit_and_resend.png';
	import etcPasswd from './etc_passwd.png';
	import solution from './solution.png';
</script>

<svelte:head>
	<title>Space Heroes CTF: Attack-Strategies</title>
</svelte:head>

<h1>Attack-Strategies</h1>
<h2>The challenge</h2>
<blockquote>
	The StarCraft III Interplanetary Newbie Championship is almost live and I was assigned to take
	care of teaching everyone in the Newbie-84 planet how to play. I made a blog so each individual
	can choose their favorite races and strategies to learn before the tournament. I will secretly
	participate and to give them a change, I hid my go to strategy somewhere on the website. Wanna try
	finding it?
</blockquote>

<h2>Solution</h2>

<p>This challenge had a web page had a form that let you select a directory and a file</p>

<img src={emptyForm} alt="empty form" />

<p>
	and after selecting a folder and file, the contents of the file just get inserted into the page.
</p>

<img src={filledInForm} alt="filled in form" />

<p>
	For more complicated challenges I like to use burpsuite to intercept requests from the browser and
	modify/replay them, however for simple challenges like this one it sometimes feels like overkill.
	Instead, I opt to just solve the challenge using the built in browser dev tools. Inspecting the
	request using the Network tab, we can see the request body that gets sent when I hit the submit
	button on the form
</p>

<img src={normalRequest} alt="normal request" />

<p>
	to mess with the request, I can just right click on it and hit <b>Edit and Resend</b> (I'm using Firefox,
	if you're on another browser then things might be very slightly different):
</p>

<img src={editAndResend} alt="edit and resend" />

<p>
	The first thing I tried was dumping a file I was sure existed: <code>/etc/passwd</code>
</p>

<img src={etcPasswd} alt="/etc/passwd" />

<p>
	Yay! It seems like I can set any file path. It took a few more guesses, but eventually I tried
	<code>./flag.txt </code> and I got the flag:
</p>

<img src={solution} alt="Solved!" />
