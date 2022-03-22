# Scavenger Hunt

## Overview

Points : 50
Category : Web Exploitation

## Description

There is some interesting information hidden around this site http://mercury.picoctf.net:5080/. Can you find it?

## Hints

1. You should have enough hints to find the files, don't run a brute forcer.

## Solve

Click On Link Then Ctrl + U or Right Click ==> View Page Source To Get Source Code

```html

<!doctype html>
<html>
  <head>
    <title>Scavenger Hunt</title>
    <link href="https://fonts.googleapis.com/css?family=Open+Sans|Roboto" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="mycss.css">
    <script type="application/javascript" src="myjs.js"></script>
  </head>

  <body>
    <div class="container">
      <header>
		<h1>Just some boring HTML</h1>
      </header>

      <button class="tablink" onclick="openTab('tabintro', this, '#222')" id="defaultOpen">How</button>
      <button class="tablink" onclick="openTab('tababout', this, '#222')">What</button>

      <div id="tabintro" class="tabcontent">
		<h3>How</h3>
		<p>How do you like my website?</p>
      </div>

      <div id="tababout" class="tabcontent">
		<h3>What</h3>
		<p>I used these to make this site: <br/>
		  HTML <br/>
		  CSS <br/>
		  JS (JavaScript)
		</p>
	<!-- Here's the first part of the flag: picoCTF{t -->
      </div>

    </div>

  </body>
</html>
```

The Comment `<!-- Here's the first part of the flag: picoCTF{t -->` Is The First Part Of Flag

Then You Get To JS,CSS File To Get Another Part

```html
<html>
  <head>
    <title>Scavenger Hunt</title>
    <link href="https://fonts.googleapis.com/css?family=Open+Sans|Roboto" rel="stylesheet">
    <link rel="stylesheet" type="text/css" href="mycss.css">
    <script type="application/javascript" src="myjs.js"></script>
  </head>
```

Click On `href="mycss.css>" or Put `/mycss.css` To URL

```css
div.container {
    width: 100%;
}

header {
    background-color: black;
    padding: 1em;
    color: white;
    clear: left;
    text-align: center;
}

body {
    font-family: Roboto;
}

h1 {
    color: white;
}

p {
    font-family: "Open Sans";
}

.tablink {
    background-color: #555;
    color: white;
    float: left;
    border: none;
    outline: none;
    cursor: pointer;
    padding: 14px 16px;
    font-size: 17px;
    width: 50%;
}

.tablink:hover {
    background-color: #777;
}

.tabcontent {
    color: #111;
    display: none;
    padding: 50px;
    text-align: center;
}

#tabintro { background-color: #ccc; }
#tababout { background-color: #ccc; }

/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */
```

The Comment `/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */` Is Second Part

Next We Get To Check The JS File

Click On `arc="myjs.js">` or Put `/myjs.js` To URL

```js
function openTab(tabName,elmnt,color) {
    var i, tabcontent, tablinks;
    tabcontent = document.getElementsByClassName("tabcontent");
    for (i = 0; i < tabcontent.length; i++) {
	tabcontent[i].style.display = "none";
    }
    tablinks = document.getElementsByClassName("tablink");
    for (i = 0; i < tablinks.length; i++) {
	tablinks[i].style.backgroundColor = "";
    }
    document.getElementById(tabName).style.display = "block";
    if(elmnt.style != null) {
	elmnt.style.backgroundColor = color;
    }
}

window.onload = function() {
    openTab('tabintro', this, '#222');
}

/* How can I keep Google from indexing my website? */
```
Now We Don't Get The Flag But Get `/* How can I keep Google from indexing my website? */`

I searched up "index website on google" and it brought up things about web crawlers. This made me think it's possible a robots exclusion file (robots.txt) might have something. I changed `myjs.js` to `robots.txt`
 `
User-agent: *
Disallow: /index.html
Part 3: t_0f_pl4c
I think this is an apache server... can you Access the next flag? `
 
Now We Got The Third Part `Part 3: t_0f_pl4c`
 
The .htacess File Manages Apache Server Permissions. Replacing `robots.txt` With `.htaccess` Got This :
 
 `Part 4: 3s_2_lO0k
  I love making websites on my Mac, I can Store a lot of information there.`
  
  What stands out the most about that hint is the capitalized "Store". In Macs, a `.DS_Store` file stores the configurations for how the desktop looks (eg. icon location, etc.) Changing `.htacess` with `.DS_Store` got
 
 `Congrats! You completed the scavenger hunt. Part 5: _35844447}`
 
 ```text
 Part 1 : picoCTF{t
 part 2 : h4ts_4_l0
 Part 3 : t_0f_pl4c
 Part 4 : 3s_2_lO0k
 Part 5 : _35844447}
 ```
 
 ## Flag
 
picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_35844447}

## Conclusion

First Go To Code There May Be Something In It Like A Sensitive Information

If He Keep Google From Indexing Her Website Write `/robots.txt` To Get Information or Another Files In Server

If Server Work In Apache Use `.htaccess`

If Server On MAC Use `.DS_Store`
 
