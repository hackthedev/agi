# Importance of a body

When wanting to create a real, learning AI, you will need a body with a few minimal capabilities, like being able to sense pressure, temperature and similar. The reason behind this is that AI, like humans, need feedback from their environment. This is very important, as this will motivate movement and therefore the AI may learn new things overtime. 

> *For example, if you sit for a while without moving, your [insert body part] may begin to feel uncomfortable or may even begin to hurt the longer you stay in that position.* 

1. Lets say a baby is lying down in bed for some time, feels uncomfortable and begin to randomly move a bit. Eventually it may turn to the side or stomach, feeling better.
2. At some point this gets uncomfortable as well, so it keeps moving and eventually ends up in a crawling position on accident as well.
3. Due to our sense of balance we know that we're not upright in that position, and it could possible feel uncomfortable  in the neck, so maybe, with more random movement, we may begin to sit or crawl.
4. With more time and more random movement and learning experiences so far, we may end up learning to stand on our legs and eventually learn walking as well.

This will require you to have a system that can save information and reuse it and basically just learn and adapt, as your AI would never be able to progress otherwise. In addition your body will need to be able to sense feedback.

------

## Body Feedback

Lets say we split every reasonable body part into modules, like your lower arm. Each module is responsible for its feedback and would something like a ESP32 with a lot of I/O Pins just as example and combine it with capacitive pressure sensing capabilities and maybe with temperature sensing.

The ESP module or whatever will be used needs to do some processing other than reading the inputs like pressure and temperature. For example the longer a pressure stays in a location, the more it gets amplified over time. Once pressure would be gone, it will slowly decrease again.

The idea now is to repeat this concept across different body parts, like hand, lower arm, ... until you have a entire body, and each ESP would send out a signals, like events roughly demonstrated below. The same would be done for other events like temperature and send to the "brain".

```json
// pressure event
{
	type: "pressure",
    part: "lower_arm",
    location: [x, y],
    value: 0.5
}

// temperature event
{
	type: "temperature",
    part: "index_finger",
    location: [x, y],
    value: 40.4 // °C
}
```

------

## The brain

At a minimum the idea is to have to processors. Potentially an Arduino Mega as cerebellum and something like a Raspberry Pi for the higher level functions. The idea is to use the Arduino for reflexes and some more processing and then send out events to the Raspberry Pi for further, final processing.

For example the arduino could check for very hot surfaces and potentially move the hand away from the heat source closer to the body as a reflex without requiring higher level processing and similar concepts. Afterwards the event will be sent to the "main brain" aka the raspberry pi for further processing, like remembering that the surface was hot and that the penalty was damage as example.

------

## Energy

Its absolutely important that the body has a sense of energy and exhaustion. For example if the body uses a battery and were to move its arm, the modules affected would constantly check for the energy before the movement and once it somewhats stops so that it creates a reference of how much energy an action took.

Based on the overall energy available its important to implement fatigue, like incrementally weakening the motor's max power, decreasing camera FPS (=eye sight) and similar so that it can be actually experienced as well. If you were to add some form of solar charging, the AI may discover that sitting still, aka resting in the sun has positive effects, whereas proper charging has a bigger impact (=sleep). 

If the AI were to move and it took a lot of energy and randomly it did the same with less energy at some point, it could use this information to learn and only use the action that requires less energy.