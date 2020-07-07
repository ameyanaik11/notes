# ITerm <> Philips Hue intergration

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
> ![Screenshot showing ITerm Trigger config](https://lh3.googleusercontent.com/fQc9Vox83bUBCdnuM6OMEvdOMsBoIqo9_kYosau5HsLPaNpe_V93K7z9Nw1kjCn7pWhLjKHOtpdo23kAoxbrFBkPx-Gp7Pu-jVuBDGHCx-yoEAz8C0TAJb05UBdf85MjpFf5cQV4ZTjBQnWWQpqmIyoE5G0hcfK91r10zqodoHpZ-Rb8y_WPqGlQNaaK9RrYK4XHG4ImutpM8nCfF6lMOKsOc358fMDfYMS1821PXUGdM39T-WhB9gjClLi_Fhf0PTdVl0Xdw3Gz0VLToZPs01jSB8TdVzwu048Ortxl2Y1eJUGp4fibsX0VuZX81JL9gQXbeTx47GkLPJASGo5WBYX_mAeFys7uDjhDeV1f4aRQ_WdSt9tnoOVTL3CTcuw9X0kVUWTQlsvgDU6dsTjzOLf5Be86_0j-Vy54ojFsRcnp6VOya0ndwrRijFrD0S_qWk2bBNgWmztUtMflxMZEZLYRXHzloMqvW2MqfG2lAvjVZtsuk_dwO_sj1ZNZqlG3l7kY75aLepBr5Iw4yNYGD4h-Vi603ofXXE8-fYOZM-hpTmmh1zhbf2od6WOl9YqKHSPU0agtHKJ4bMmR_R8U3JqKFE5zESjQ06owXdYvcwXL9gdgPJNV-eKBhxe55hSEhS-0dQsRlq60b3Us5BOYGSfiRlzQtgfJiaWaielOYVdFQn8WFhTq2bMH8lGlFg=w928-h442-no?authuser=0)
