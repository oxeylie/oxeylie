<div align="center">	
<img width="3839" height="1200" alt="Cherry_Blossom copy" src="https://github.com/user-attachments/assets/8c1e3fdd-ea4b-4964-b88c-32568e1f83dd" />
<h1>Hi, I'm Oxeylie 🌸 <i>(fka Kcraft⁰⁵⁹)</i></h1>

</div>

First, I wanted to thank you for taking the time to look a bit at my profile, I'm sure it's quite uncommon ^^'…

# Bio:
If anything at all I'm just a curious person who loves computers and science stuff ^^!
I'd rather be called using `they/them` but it's not a big deal if you're using smth else.  
I'm currently studying with the goal of maybe becoming an engineer (if lucky enough), so I'm quite busy most of the time.  
Not absolutely opposed to the use of AI, tho only for ethical purpose it is to say, I **don't** vibe code.

<details>
<summary><i><b>Interests</b></i></summary><br>
	
I got told since I was young how curious I was… 
So as the years went by and as I felt progressively more capable of dealing with complicated subjects, my interests for maths, physics, and IT grew along.
Later this turned into my passion for IT and lately <b>low level programming</b>.
To this very day I'm eager to learn in the subjects that interest me. <br>
<i>(yeah… that means I did go through ≈600 pages of documentation on the atmega328p to try and understand the role of each of its registers "for fun" ;-;)</i><br>
	
While I don't claim to have anywhere near the knowledge of a real dev, during the years I had the opportunity to learn a few key concepts that helped me in my little projects ^^! 
</details>

<details>
<summary><i><b>Experience</b></i></summary><br>
	
The only real experience I've had was really only through my own research, but they were quite varied.<br>
	
My first introduction to programming was really only a few bash scripts… but I quickly got the idea to learn a <i>real</i> language. So I decided to try and learn some python… at the beginning I did understand the language in itself… but had no idea how it really worked under the hood… But that didn't bother me at the time as I just got into programming ^^.<br>
	
Later the idea of making a website got me… my goal at first was to make it pretty… but I quickly understood that it wasn't really what motivated me. I wanted to some real programming, I wanted to try and do a bit of backend. I went as far as doing a somewhat functional user/group/policy object-oriented system with a database and all but… at some point I lost interest for the backend so it really only ended in: <br>
	
```php
<?php
  http_response_code(404);
  echo "Oh… I might have not implemented this yet - swy";
?>
```

The real reason for the loss of interest is because I started to wonder if I could get into <b>low-level</b> programming like C to understand how things really worked under the hood ^^.<br>

```c
#include <stdio.h> // Import definitions for different libs
#include <string.h>
#include <stdlib.h>

int main(int argc, char** argv) { // And this time I actually started to comment my code 
  char* string = malloc(sizeof(char) * 5); // Alloc mem on heap for string, and yeah I didn't do proper checks for NULL at the time
  memcpy(string,"Yeah", sizeof(char) * 5); // Copy mem from address of immediate "Yeah" to string, on 5 bytes
  printf("%s, after php, c did taste harder ^^'\n",string); // Print to stdout replacing %s which the string in string
  free(string); // Free mem
}
```

From this point on I started to understand key concepts in how a computer worked with, data, computations etc… So I tried re-implementing some concepts by myself as a little challenge: dynamic arrays, hashmaps & quick-sort. <br>
After that, I knew I wanted to go deeper… So I tried my hand at assembly on a fairly simple but interesting architecture, `avr` (arch most Arduinos runs on). <br>
As usual I wanted to try and re-implement as best as I could some basic systems that make programming what it is nowadays, so I tried making a memory allocator from scratch in asm. Alongside this I learnt how to interact with IO registers to create pulses, signals based on clocks etc… 

```asm
#include <avr/io.h>
.section .vectors              ; Interrupt vector table
.org 0x0000
	jmp init                     ; On reset jump to init
.section .text
init:
	ldi r16, lo8(RAMEND)         ; Init Stack pointer
	out _SFR_IO_ADDR(SPL), r16
	ldi r16, hi8(RAMEND)
	out _SFR_IO_ADDR(SPH), r16
	rcall led_on                 ; Call led_on subroutine
end:
	rjmp end                     ; End loop, halt execution
led_on:
	sbi _SFR_IO_ADDR(DDRB), DDB5 ; Set bit for pin 5 port B in data direction reg
	sbi _SFR_IO_ADDR(PORTB), PB5 ; Set bit for pin 5 port B in port register
	ret                          ; Set instruction pointer to the address on stack from which subroutine has been called 
```
And that's pretty much all I got for now

<b><i>Sidenote on nix:</i></b>

I also use nix, not as a general purpose language but rather for its most frequent use, as a package manager. I got into nix, for a really dumb reason, I needed a reproducible environment because I kept breaking my OS by experimenting at the point where a reinstall was quicker. So I got into nix pretty early in all this but it gave me the opportunity to test pretty much any language & any package thanks to the sheer amount of packages it offers.<br>
This convenience had a cost tho since…

```nix
{pkgs, lib, ...} :
{
  service.readme = {
    enable = true;
    config.welcomeMsg = "Nix has a steeper learning curve than it seems…";
  };
}
```
</details>

<details>
	<summary><i><b>Projects</b></i></summary>
I've only got a few real projects apart from experimenting languages and learning things. The most significant for now was my attempt at building a proper website… which… only got so far. I later went and restarted the project on a better base in go and it's still undergoing development.<br>
	
Alongside my website I ofc needed a little home-server setup so I did make one using NixOS which was really interesting! <br> 

Hopefully my next big project (it's relative) is to make a little TUI (ascii-style graphics) multiplayer game named Amaze where I want to implement a simplistic 3d engine by myself ^^!
</details>

# TL;DR:

__To make it quick here's a recap:__
```yaml
# Yk what, a yaml will do the job better than me
Name: Camille / Oxeylie
Pronouns: they/them # TODO: debug genderd.service
Age: 17
Spoken languages: en / fr
Languages:
 - c
 - go
 - asm (on avr)
OSes:
 - GNU linux (especially NixOS)
 - macOS
```

> To anyone who reached this far, I wish you the best! And I would also give a special thanks to the open-source community and to a lot of people who are much more talented than me who led me into being able to do so much !  
> \- _Oxeylie_

> [!NOTE]
> If you want to contact me you can do it over Discord[^1], and expect an answer within 24h

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

[^1]: Id: @oxeylie, message requests opened.
