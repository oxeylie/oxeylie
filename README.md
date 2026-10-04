<div align="center">	
	
<h1>Hi ! 🌸 So want to know me a bit more ?</h1>
<img width="1470" height="956" alt="Screenshot 2025-11-13 at 18 14 15" src="https://github.com/user-attachments/assets/f310f5b2-3ba2-4bc0-a9d5-e4d0f45a7518" />

> → _The future \*might be\* declarative._

</div>

## Me

So, as I said, **Hi there !!** 👋<br>
But let's start with a few formalities first:

```yaml
# Few elements about me 
Name: Camille
Pronouns: they/them # TODO: debug genderd.service
Nationality: 🇫🇷
Age: 17
Languages: # I don't master any of those 
 - C 	  # I'm trying to focus on low-level compiled languages for now
 - Nix    # Mainly for env config & dev shells
 - PHP    # (alongside other front-end languages like JS)
 - Bash / Zsh
 - Python # I don't use it that much anymore
 - Go     # For an upcoming version of my website
 - ASM    # (On avr)
```
> Yeah… on the moment I thought this would look good… Yeah strange profile for a strange person…

Anyway, I'm Camille, I also go by `Oxeylie` (formerly `Kcraft059`) online, I'm a french high-school student who codes in their free time. My english isn't perfect 😅, but I love practicing it as much as I love talking to people.<br>
I’m interested in pretty much every tech domain, though lately I started to specifically dive into <b>low-level programming</b>. I use macOS (because it's UNIX-like - tho let's be honest it's extremely restrictive[^1]) in combination with Nix-Darwin to fully configure my system in a reproducible way.

## My Journey

<details>
<summary>But let's start at the beginning of my journey, shall we ?</summary>
<br>
It started relatively simple, an old piece of junk: my <b>Late 2012 MacMini</b>.<br>
This piece of tech gave me the passion I have today for IT. It started with a few teardowns & rebuild, which made me want to experiment more like forcing macOS suppport through <b>OCLP</b>, installation of <b>Ubuntu</b> on dual boot, all those which helped me understand how computers worked more in depth !<br>
Tho it was not without mistakes… I did screw-up my macOS instances a few time 🥲, and made more reinstalls than any sane person should do 🫠<br>
<br>
This is where it took a turn when I discovered Nix, a reproducible & declarative package manager (this seemed perfect given how often I reinstalled macos).<br>
I made a config… and soon realised I fell into a rabbit hole as I found myself digging into docs at 2am swearing at a scope bug because I did not pass an input… (true 'me' fashion tbh 🥰)

```nix
{pkgs, lib, ...} :
{
  service.readme = {
    enable = true;
    config.welcomeMsg = "Nix has a steep learning curve… "; # And at the time, the hardest thing I ever done was a for loop in bash
  };
}

```

After I made this config, I saw the potential I had in my hands, access to unlimited packages, and a growing interest for programming !<br>

At some point after, I got the idea of making a <b>website</b>. At the time I only had a vague idea of what it consisted of... a server, a software to run the server ?<br>
I made a few research, I already had the idea to install a headless NixOS version on my MacMini which I knew I'd soon replace with a new Mac Book Air. And so, I made a config in nix, I chose a <b>LEMP</b> stack and got to coding !<br>
The months that followed were really interesting, I learned how to manage a server, how to use ssh etc… The next step being the website itself, I started to get into html, css, php & sql, at some point I even made a full framework for a user system in <b>OOP</b> !<br>

Tho the frontend to those backend features… is… let's say it's still pending 🙄

```php
<?php
  http_response_code(404);
  echo "Oh… I might have not implemented this yet - swy";
?>
```

Following this experience, I started to wonder if I could get into <b>low-level</b> programming like C... so I <b>tried</b> !<br>
This helped me understand how things really worked under the hood ^^.<br>
I then did a few libs (implementing dynamic arrays & hasmaps from scratch) where I implemented the concepts I found tricky in C, pointers, type size & mem alloc. (I'm quite proud of those ngl 😅 !)

```c
#include <stdio.h> // Import definitions for different libs
#include <string.h>
#include <stdlib.h>

int main(int argc, char** argv) { // And this time I actually started to comment my code 
  char* string = malloc(sizeof(char) * 5); // Alloc mem on heap for string
  memcpy(string,"Yeah", sizeof(char) * 5); // Copies mem from adress of "Yeah" to string, on 5 bytes

  printf("%s, after php, c did taste harder ^^'\n",string); // Print to stdout replacing %s which the string in string

  free(string); // Free mem, make it usable again by any other part of the computer  
}
```

So yeah, not much in fact 😅, but I'm learning things and having fun doing so and this might be the most important thing to remenber !<br>
As of today I'm really proud of how far I've gone and I realize everyday how much I still have to learn. But looking back at my knowledge from a year ago, I only am more confident that with time I'll improve my skills !

> I know this is a bit unusual for a Github Profile, but I mean, my profile, my decisions ¯\\\_(ツ)\_/¯

</details>

## Nowadays
**My 'projects' :**

- ⚙️ Low level [programing in C](<https://www.github.com/kcraft059/c-lang-playground>)
- 🌐 An unfinished [website](<https://ftnetwork.duckdns.org/>)
-	🛠️ A sketchybar [config](<https://www.github.com/kcraft059/sketchybar-config>)
-	📋 A declarative Nix [config](<https://www.github.com/kcraft059/Nix-Config/>)
- 🇬🇧 Help in the translation of [BetterDisplay](<https://www.github.com/waydabber/betterdisplay>)

## TL;DR :

_A silly kid trying to learn IT by themselves, coding on feelings & doing things in the most complicated way possible.
You might just wanna see ppl more talented than me… ^^'_

> [!NOTE]
> If you want to contact me you can do it over Discord[^2], and expect an answer within 24h ^^!

## Hardware / OSes

**Oses that I use :**
- [x] MacOS [Main] - managed through Nix-Darwin
- [x] NixOS - For my server
- [x] Windows - only when i'm forced to…
- [ ] Ubuntu - I don't really use it anymore
- [ ] Asahi Linux - _(I hope a release for M3 macs comes out !)_

**My hardware :**
- Laptop : [Arm64] `Macbook Air M3 (2024)`
- Server : [x86] `Mac Mini Late 2012` x2
- _And a lot more junk that doesn't need to be displayed here 😅…_

---


```
	   .-'~~~-.
	 .'o  oOOOo`.
	:~~~-.oOo   o`.
	`. \ ~-.  oOOo.
	  `.; / ~.  OO:
	 .'  ;-- `.o.'
	,'  ; ~~--'~
	;  ;
_ \\;_\\//___\|/_ __  _    _
```
_“As the reality slowly decays… „_

[^1]: Tho a little `csrutil disable; csrutil authenticated-root disable` makes it surrender easily 🥰
[^2]: Id: @kcraft059, message requests opened.
