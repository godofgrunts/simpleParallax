# simpleParallax

A simple parallax library I made for learning. Hopefully it will be usefull for my games as well.


# How to

Throw the whole libs directory in the same directory as your main.lua (it expects camera.lua to be like ./libs/camera.lua)

    newParallax(image, speed, x, y, zoom)

This creates two tables. var.a and var.b. This is so you can loop them

    loopScene(newParallaxTable, offset)

# Example

```lua
local par = require 'libs/simpleParallax'

function love.load()
  farBldg = love.graphics.newImage('bldg1.png')
  medBldg = love.graphics.newImage('bldg2.png')
  cloBldg = love.graphics.newImage('bldg3.png')
  far = par.newParallax(farBldg, 20, 0, 0, 3.5)
  med = par.newParallax(medBldg, 60, 0, 0, 3.5)
  clo = par.newParallax(cloBldg, 100, 0, 0, 3.5)
end

function love.draw()

  far.camera:attach()
    love.graphics.draw(far.a.img, far.a.x, far.a.y, 0, 1, 1)
    love.graphics.draw(far.b.img, far.b.x, far.b.y, 0, 1, 1)
  far.camera:detach()

  med.camera:attach()
    love.graphics.draw(med.a.img, med.a.x, med.a.y, 0, 1, 1)
    love.graphics.draw(med.b.img, med.b.x, med.b.y, 0, 1, 1)
  med.camera:detach()

  clo.camera:attach()
    love.graphics.draw(clo.a.img, clo.a.x, clo.a.y, 0, 1, 1)
    love.graphics.draw(clo.b.img, clo.b.x, clo.b.y, 0, 1, 1)
  clo.camera:detach()

end

function love.update(dt)

  if player.x + 90 < playerCam.x then
    playerCam:move(-player.speed * dt,0)
    far.camera:move(-far.a.speed * dt,0)
    med.camera:move(-med.a.speed * dt,0)
    clo.camera:move(-clo.a.speed * dt,0)
  end

  far = par.loopScene(far, 50)
  med = par.loopScene(med, 0)
  clo = par.loopScene(clo, 0)

end
```

Also, see [parallaxDemo](https://github.com/godofgrunts/parallaxDemo) for a working example.
