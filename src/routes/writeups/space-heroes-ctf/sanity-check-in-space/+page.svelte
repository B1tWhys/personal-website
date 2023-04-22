<script>
	import firstPage from './first_page.png';
	import robots from './robots.png';
	import humans from './humans.png';
	import cookies1 from './cookies_screenshot_1.png';
	import cookies2 from './cookies_screenshot_2.png';
	import arrakis from './arrakis.png';
	import arrakisHtml from './arrakis_html.png';
	import arrakisSolved from './arrakis_solved.png';
	import pingGoogle from './ping_google.png';
	import pingLsInjection from './ping_ls_injection.png';
	import catInjection from './ping_cat_injection.png';
</script>

<svelte:head>
	<title>Space Heroes CTF: Sanity Check in Space</title>
</svelte:head>

<h1>Sanity Check In Space</h1>
<h2>The challenge</h2>
<blockquote>
	Man, web exploitation sure is fun. Sometimes you just need to go back to the basics, you know what
	I mean? Everything you need to get started on your journey to becoming a web master is here.
	<br />
	p.s: You can make anything space themed if you try hard enough.
</blockquote>

<h2>Solution</h2>
The first page of this challenge prominantly featured a picture of a robot:

<img src={firstPage} alt="first page screenshot" class="h-96 m-auto" />

which was a pretty clear hint to check the robots.txt file. Sure enough, there's a message to be
found there

<img src={robots} alt="robots.txt screenshot" />

The trailing <code>humans.txt/</code> looks like a hint to try going to
<code>/humans.txt</code>, and sure enough there's another hint waiting:

<img src={humans} alt="humans.txt screenshot" />

My first thought seeing a tasty cookie front and center like that was to check if there were any new
cookies in the browser dev tools, and sure enough a brand new <code>human</code>
cookie was waiting for me, set to <code>false</code>

<img src={cookies1} alt="a new cookie appears!" />

I changed the value to true, and was rewarded with a new hint
<img src={cookies2} alt="a new message" />

The reference was initially lost on me, but after a quick google it turns out
<a href="https://en.wikipedia.org/wiki/Arrakis">Arrakis</a>
is the desert plannet from Dune. Anyhoo, the next page of the challenge was (as you'd expect) at
<code>/arrakis</code>

<img src={arrakis} alt="arrakis" />

Finally we're greeted with something interactive! I tried a few sql injections, but didn't get
anything promising so I took a look at the HTML for comments and was rewarded with the password

<img src={arrakisHtml} alt="arrakisHtml" />

Entering that into the password field I got another hint

<img src={arrakisSolved} alt="arrakis solved" />

On to <code>/krypton</code>!

<img src={pingGoogle} alt="ping google" />

Entering <code>google.com</code> into the form, we're met with the familiar output of the posix
<code>ping</code>
utility. Under the hood, I assumed that what's going on here is that the server is simply running
<code>ping &lt;USER INPUT&gt;</code>
on the command line. If so, then it's vulnerable to command injection! I tested this by entering
<code>; ls</code>
and was rewarded with a list of files, including <code>flag.txt</code>!

<img src={pingLsInjection} alt="listing files" />

To complete the challenge, I just had to print the flag by injecting <code>; cat flag.txt</code>

<img src={catInjection} alt="cat injection" />
