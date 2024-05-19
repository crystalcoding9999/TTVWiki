On this page you can find all computercraft methods

!!! info
    These methods require the computercraft or CC:Tweaked mod!

---

## enableThrottle()

When this method is called the throttle will be enabled

`returns -> Boolean`

---

## disableThrottle()

When this method is called the throttle will be disabled

`returns -> Boolean`

---

## readyToLand()

This method will return true if the TARDIS is ready to land (Only necessary in BOTI TARDIS)

`returns -> Boolean`

---

## isFlying()

This method will return true if the throttle is currently enabled

`returns -> Boolean`

---

## getFlightTime()

This method will return the time left in the current flight.

`returns -> Integer`

---

## setCoords(String coords)

This method takes a string in the format of `123 69 -420` (`X Y Z`) and sets the coordinates accordingly,
<br><br>
Will return false if the coordinates are not formatted correctly,
<br>
Will return true if the coordinates were set correctly.

`returns -> Boolean`

---

## setDimension(String dimension)

This method takes the lowercase id of a dimension and sets it accordingly.
<br><br>
For example the overworld is "overworld" and the end is "the_end".
<br>
you can find a list of the dimension names by typing "/execute in " and looking at the recommended options. 
<br>
Simply use everything after the colon.
<br><br>
Will always return true.

`returns -> Boolean`

---

## getTargetLocation()

This method will return the current Target location as a table: `
{
    x=x,
    y=y,
    z=z
}
`

`returns -> Table`

---

## getExtLocation()

This method will return the current position of the TARDIS as a table: `
{
    x=x,
    y=y,
    z=z
}
`

`returns -> Table`

---

## getTargetDimension()

This method will return the current target dimension

`returns -> String`

---

## getExtDimension()

This method returns the dimension the TARDIS is currently in

`returns -> String`

---

## getTargetRotation()

This method will return the current target rotation of the TARDIS

`returns -> String`

---

## getTargetBlock()

This method will return the name of the block you would replace if you landed there

`returns -> String`

---

## setSign(String text)

This method changes the exterior sign text of the TARDIS
<br>
This text must be 16 characters or less.
<br><br>
The returned boolean will be true if set and false otherwise

`returns -> Boolean`
