# Ancient C compilers

Stackoverflow, while a really great site, sometimes has a SPAM policy that is a bit too strict. Of course, it is logically they want to prevent people from advocating their own software. A question that would initiate a lot of answers regarding pointers to different ancient C compilers and would be a great resource for people online, [can not make it](https://stackoverflow.com/questions/25266909/where-is-the-source-code-for-the-earliest-c-compilers).

## Why bother about old code?

Links to old code give at times quite some authority to a question. See this reference to an analysis of source code of an early compiler, e.g.:

* [Why was the switch statement designed to need a break? where is referred to the Sun ANSI C compiler front end](https://stackoverflow.com/questions/252489/why-was-the-switch-statement-designed-to-need-a-break) by Peter van der Linden.

If you really want to know why `switch` statements have breaks or why other choices have been made, it might be worthwhile to look how they were used in the code. For example, I see a lot of fall-throughs in this code! Off-topic, but I think the real reason is different. A `switch` statement is quite a "flat" structure. A person who likes a `switch` statement does probably not like a piece of code like this (with implicit breaks):

	switch(p) {
	case 0: 
		if (error_cond1) {
			// do something
		} else {
			if (error_cond2) {
				// do something
			} else {
				// do something
			}
		}
	case 1:
		// do something
	}

But probably more like this:

	switch(p) {
	case 0:
		if (error_cond1) {
			break;
		} 
		if (error_cond2) {
			break;
		} 
		// do something
		break;
	case 1:
		// do something
		break;	
	}

Just my two cents, but I personally understand why people who love switches would love breaks as well, especially if the horizontal screen estate was much more limited in those days.

A quick `pcregrep -Mi 'case.*\n.*case' * | wc -l` in the `c` directory shows `166` fall-throughs by the way, and these are only subsequent `case` statements on subsequent lines. I would say, that's quite a lot on a total of `grep -ri case . | wc -l`: `459`. 

# Source code

References to source code of early compilers:

* Sixth edition of Unix by Bell laboratories released in May 1975, which is designed to run on the PDP-11. The [files](http://minnie.tuhs.org/Archive/PDP-11/Distributions/research/Dennis_v6/) are from [Dennis Ritchie](https://en.wikipedia.org/wiki/Dennis_Ritchie). The compiler can be found in the `c/` directory.
* Ritchie [describes](http://www.cs.bell-labs.com/who/dmr/primevalC.html) a DECtape found by Paul Vixie and Keith Bostic. Which can be found on github elsewhere as well as [legacy-cc](https://github.com/mortdeus/legacy-cc). To honor Ritchie it is here added in his words as "primeval C".

# Todo

Cardeva made a lot of source available on the Unix Archive, e.g. see the [minnie.tush.org mirror](http://www.tuhs.org/Archive/PDP-11/Distributions/). Interesting code needs to be extracted from there.

# Documentation

* https://en.wikipedia.org/wiki/Portable_C_Compiler by Stephen C. Johnson of Bell labs in mid seventies
* https://en.wikipedia.org/wiki/Amsterdam_Compiler_Kit by Andrew Tanenbaum in early eighties (but not open-source of course, or we wouldn't have had gcc)
* https://en.wikipedia.org/wiki/GNU_Compiler_Collection by Richard Stallman in 1987

