On this page you can find a few example scripts

## TARDIS recall script

This script will allow you to move your TARDIS using a pocket computer

<br>
<br>

For this script you will need:
<br>
1. Computer
<br>
2. Ender Modem
<br>
3. Ender pocket computer

<br>

It does not matter whether the Computer and Ender Pocket Computer are Advanced or not

<br>
First the code for the computer that is connected to the Time Vortex Interface

```lua title="computer.lua" linenums="1"
peripheral.find("modem", rednet.open)
local tardis = peripheral.find("vortexmod:vortex_interface_be") or error("No Time Vortex Interfce connected!")

while true do
    id, message = rednet.receive()
    
    x = message.x
    y = message.y
    z = message.z
    dimension = message.dim
    
    tardis.setCoords(x.. " ".. y.. " ".. z)
    tardis.setDimension(dimension)
    
    if tardis.enableThrottle() then
        rednet.send(0, {status="success"})
        
        -- ensures tardis does not stay in the time vortex when auto land is disabled
        repeat
            sleep()
        until tardis.readyToLand()
        
        sleep(0.1)
        
        tardis.disableThrottle()
    else
        rednet.send(0, {status="failed"})
    end
end
```
<br>
Then the code for the Ender Pocket Computer
<br>
Make sure to change the value of `tardis_id` to the id of the computer connected to the Time Vortex Interface

```lua title="pocket.lua" linenums="1"
rednet.open("back")

local tardis_id = 1

while true do
    print("What X am I going to?")
    local x_number = tonumber(read())
    if x_number ~= nil then
       print("What Y am I going to?")
       local y_number = tonumber(read())
       if y_number ~= nil then
           print("What Z am I going to?")
           local z_number = tonumber(read())
           if z_number ~= nil then
               print("What dimension am I going to?")
               local dimension_string = read()
               local data = {x=x_number, y=y_number, z=z_number, dim=dimension_string}    
               rednet.send(tardis_id, data)
               print("Packet sent")
               id, message = rednet.receive()
               term.clear()
               term.setCursorPos(1, 1)
               print(message.status)
           end
       end 
    end
end
```

## TARDIS control panel

This script will let you have the functionality of a keypad without needing a keypad

<br>

For this script you will only need a computer, advanced is not required

```lua title="panel.lua" linenums="1"
local tardis = peripheral.find("vortexmod:vortex_interface_be")

while true do
    local currentTar = tardis.getTargetLocation()
    local currentPos = tardis.getExtLocation()

    term.setCursorPos(1,1)
    term.clear()
    print("Current Position: ".. currentPos.x .. " " .. currentPos.y .. " " .. currentPos.z)
    print("Current Target: ".. currentTar.x .. " " .. currentTar.y .. " " .. currentTar.z)


    print("Enter X coordinate (~ to leave unchanged): ")
    local x = read()
    if x == "~" then
        x = currentTar.x
    else
        x = tonumber(x)
    end

    print("Enter Y coordinate (~ to leave unchanged): ")
    local y = read()
    if y == "~" then
        y = currentTar.y
    else
        y = tonumber(y)
    end

    print("Enter Z coordinate (~ to leave unchanged): ")
    local z = read()
    if z == "~" then
        z = currentTar.z
    else
        z = tonumber(z)
    end

    tardis.setCoords(x .. " " .. y .. " " .. z)

    print("Enable auto pilot? (y/N)")

    if (read() == "y") then
        tardis.enableThrottle()
        
        term.clear()
        term.setCursorPos(1,1)

        print("Travelling to " .. x .. " " .. y .. " " .. z)
        repeat
            term.setCursorPos(1,2)
            term.clearLine()
            print("ETA " .. tardis.getFlightTime())
            sleep()
        until tardis.readyToLand()

        sleep(.1)
        tardis.disableThrottle()
    end

end
```
