On this page you can find a few example scripts

## TARDIS recall script

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
