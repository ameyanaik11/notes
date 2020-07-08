# Intergration Philips Hue with ITerm

## Why {docsify-ignore}

As developer, I spend signifiant time with Bash (thats iTerm2 for me) debugging / compiling random things / running though code reviews.

The integration with Philips Hue offers me real-time associate, mainly informing me when terminal needs my attention.

## Usecases {docsify-ignore}

Set my monitor lights:
- Color loop when terminal needs inputs, e.g. "Confirm y/n: ..."
- Red when compliation fails
- White when compilation is successful, e.g I can test things in browser

## Bash script helper {docsify-ignore}

- Install [Hue-shell](http://josef-friedrich.github.io/Hue-shell/installation.html), which enables UNIX shell scripts to control the Philips Hue.
- Create a helper Bash script

```shell
#!/bin/bash

if [ "$1" = "async" ]; then
  # Trigger - Pushing changes to staging area
  /usr/local/bin/hue set 13 --on --bri 250 --effect colorloop --sat 250
elif [ "$1" = "compiling" ]; then
  /usr/local/bin/hue set 13 --on --bri 250 --effect colorloop --sat 250
elif [ "$1" = "compiled" ]; then
  /usr/local/bin/hue set 13 --on --effect none
  /usr/local/bin/hue set 13 --on --hue 42354 --sat 66
elif [ "$1" = "confirm" ]; then
  /usr/local/bin/hue set 13 --on --bri 250 --effect colorloop --sat 250
elif [ "$1" = "failed" ]; then
  /usr/local/bin/hue set 13 --on --bri 250 --hue 0 --sat 250
elif [ "$1" = "clear" ]; then
  /usr/local/bin/hue set 13 --on --effect none
  /usr/local/bin/hue set 13 --on --hue 42354 --sat 66
elif [ "$1" = "success" ]; then
  # Trigger - Created a new Differential revision
  /usr/local/bin/hue set 13 --on --effect none
  /usr/local/bin/hue set 13 --on --hue 42354 --sat 66
fi
```
- Configure [ITerm Trigger](https://iterm2.com/documentation-triggers.html) to Run this shell script.
> ![Screenshot showing ITerm Trigger config](https://lh3.googleusercontent.com/pw/ACtC-3fUMprU_ILbrxUzTCrA3wHkqDRY8D87Oq2k96ON2fPhztAeXgKfMLq0ee4glsJ6rvVToP5Q0oRPrnnSUTBKCoFpxHqf_GWnmHkm1b9yEZ6QIK-iZQ1vJKzF-GxZLmaeXYK79l4TgfADujMwcnSyRGXOmQ=w928-h442-no?authuser=0)
