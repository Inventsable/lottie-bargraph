# lottie bar graph ([original request](https://github.com/airbnb/lottie-web/issues/1919))

![](./src/assets/screenshot.png)

## [Online demo here](https://keen-noether-1fd6f1.netlify.com/#/)

---

- [AEP file](./graph.aep)
- [Example lottie api registration]()
- [Issue reference for slider controls in lottie-api](https://github.com/bodymovin/lottie-api/issues/6)

---

## Notes on AEP:

The bars are created with simple rectangles with expressions attached to slider controls:

Size: 
```js
// [width, height]
[30, thisComp.layer("graphValues").effect("x")("Slider") * 3]
```

Position:
```js
// [xPosition, yPosition]
[0, thisComp.layer("graphValues").effect("x")("Slider") * -1.5]
```

Notice that the y position and height use the same value, but the yPosition is effectively bumped up by half the offset value (creating the illusion of the bar only growing from the bottom up).

Since lottie-api value callbacks happen after the animation mounts, it'd probably be best to:

- Have no keyframes (since you must have the animation playing for the api to control it in realtime)
- Have your bargraph values rendered starting at 0 (since there's a noticeable blink between their initial state and the value once the api hits)

--- 

## Requirements

- lottie-web
- lottie-api