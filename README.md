Warning! Experimental code!

Hue shell is a collection of shell scripts to control the Hue lamps from
Philips (https://www.meethue.com). Hue shell runs on many shells (sh, dash, ash, bash) and UNIX operating systems (Linux, MacOS X, FreeBSD, OpenWRT). 

NAME
        hue - control the Hue lights from Philips using a unix shell.

SYNOPSIS
        hue <command> <options>

DESCRIPTION
        Hue-Shell is a shell script to control the Hue lamps from
        Philips (https://www.meethue.com).

REQUIREMENTS
        curl

INSTALLATION

    git clone git@github.com:Josef-Friedrich/Hue-shell.git $HOME/Hue-shell
    ln -s $HOME/Hue-shell/config/hue-shell.conf /etc/hue-shell
    ln -s $HOME/Hue-shell/startup/SysVinit /etc/init.d/hue

You have to set an username. Use this documentation for.
    http://www.developers.meethue.com/documentation/getting-started

You need a working Philips Hue setup, the IP address of your
bridge and a username to access the bridge. Please read
http://developers.meethue.com/gettingstarted.html for more
informations to achieve that. Than edit the file 'hue' and fill
in the values for IP and USERNAME.


https://github.com/wertarbyte/triggerhappy

    cd /etc/triggerhappy/triggers.d
    ln -s $HOME/hue-shell/config/triggerhappy.conf


########################################################################
# HUE SET
########################################################################

```
Usage: hue set <lights> <options>

OPTIONS

        --on
                On state of the light.

        --off
                Off state of the light.

        -b, --bri, --brightness
                The brightness value to set the light to. Brightness is
                a scale from 0 (the minimum the light is capable of) to
                255 (the maximum). Note: a brightness of 0 is not off.

        -h, --hue
                The hue value to set light to. The hue value is a
                wrapping value between 0 and 65535. Both 0 and 65535 are
                red, 25500 is green and 46920 is blue.

        -H, --help
                Show this help text.

        -s, --sat, --saturation
                Saturation of the light. 255 is the most saturated
                (colored) and 0 is the least saturated (white).

        -x
                The x coordinates in CIE color space.

        -y
                The y coordinates in CIE color space.

                Both x and y must be between 0 and 1. If the specified
                coordinates are not in the CIE color space, the closest
                color to the coordinates will be chosen.

        -c, --ct
                The Mired Color temperature of the light. 2012 connected
                lights are capable of 153 (6500K) to 500 (2000K).

        -a, --alert
                The alert effect, is a temporary change to the bulb’s
                state, and has one of the following values:
                  “none” – The light is not performing an alert effect.
                  “select” – The light is performing one breathe cycle.
                  “lselect” – The light is performing breathe cycles for
                  30 seconds or until an “none” command is received.

        -e, --effect
                The dynamic effect of the light. Currently “none” and
                “colorloop” are supported. Other values will generate an
                error of type 7.
                Setting the effect to colorloop will cycle through all
                hues using the current brightness and saturation
                settings.

        -t, --transitiontime
                The duration of the transition from the light’s current
                state to the new state. This is given as a multiple of
                100ms and defaults to 4 (400ms).

EXAMPLES
        hue set 1,2,3 --alert
        hue set all --hue 23456 --bri 123 --sat 234

```

########################################################################
# HUE RECIPE
########################################################################

```
Usage: hue recipe <option>

DESCRIPTION
        This scene command shows white colors in different color
        temperatures. All lights displaying the same color temperature.

OPTIONS (only one option is possible)
        -c, --concentrate
                This option creates a light situation best for
                concentrating. It show a medium cold color temperature.

        -d, --default
                Show the default white color temperature, which the
                lights showing, when they turned on.

        -e, --energize
                The option 'energize' produces the coldest white color
                of all recipes.

        -h, --help
                Show this help text.

        -R, --reading
                The hue lights displaying a medium warm white color
                temperature, which is good for reading.

        -r, --relax
                Let the hue lights shine in a very warm white color,
                which is optimized for relaxing.

SORTING BY COLOR TEMPERATURE
        COLD -> energize (156) -> concentrate (233) -> readintg (346)
        -> default (369) -> relax (443) -> WARM

        The numbers in parentheses are Mired color temperature values.6)
        -> default (369) -> relax (443) -> WARM

EXAMPLES
        hue recipe --reading
        hue recipe -r
```
