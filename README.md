# Handylib - by TheCookingSenpai

## An handy library for Love2D that allows you to create and manage buttons and other GUI elements easily

### Install & Usage

Just download handylib.lua and put it in your project directory.
Then, you just need to:

    local handy = require("handylib")

### Requirements

- LUA (duh)
- Love2D (duh x2)
- Lovebrew ([https://lovebrew.org/](https://lovebrew.org/))
- Some patience to learn the basics of love2d and lovebrew
- Possibly a Nintendo 3DS

### Buttons

#### Methods

- addButton(name, text, x, y, size, image, callback)
- removeButton(name)
- checkButton(x, y)
- buttonExists(name)
- callButtonName(name)
- callButtonIndex(index)

#### Logic

A 400x240 navigation table is created, as well as a buttons table.
The navigation table is used to check if a button exists at a certain position.
The buttons table is used to store the button data.

The buttons have a name, a text (the one appearing in the GUI itself), an image and a callback function
that is called when the button is pressed.

Every button occupies a certain area in the navigation table, based on the starting position
and the size of the button. A 20x20 button at position 100,200 would occupy 20x20 cells in
the navigation table starting from 100,200 to 120,220.

Using the classic Love2D callback functions, is possible to check if a button is pressed, clicked,
hovered, released and so on.

Thanks to the cursor property it is also possible to navigate through the buttons using the dpad
by increasing or decreasing the cursor value and using the callButtonIndex method.
This is useful to enable a non-touch navigation system (or an hybrid one).

#### Example

This snippet shows how to add a button to the GUI from any script that includes
handylib.

    local addButton = function (name, text, image, callback, x, y)
        if not handy:buttonExists(name) then
            local testButtonImage = love.graphics.newImage(Program.Attributes.AssetsFolder .. image)
            local size_x = testButtonImage:getWidth()
            local size_y = testButtonImage:getHeight()
            handy:addButton(name, text, x, y, {size_x, size_y}, testButtonImage,
                            callback)
            local textPosition = {x + handy.buttons[name].size[1]/3, y + handy.buttons[name].size[2]/4}
            love.graphics.draw(handy.buttons[name].image, x, y)
            love.graphics.print(handy.buttons[name].text, textPosition[1], textPosition[2])
            return true
        end
        return false
    end

### Other GUI elements

Work in progress.

### License

This library is released under the Creative Common BY-NC-SA license 4.0.

You can obtain a copy of the license at [https://creativecommons.org/licenses/by-nc-sa/4.0/](https://creativecommons.org/licenses/by-nc-sa/4.0/).
