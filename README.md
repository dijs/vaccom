[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)

### Vaccom

A module for controlling the Roomba iCreate 2 robot.

Built to make vacuum robot programming easy!

**Documentation is also published and can be generated from the project.**

Music Example:
```js
import {serialOpen, serialClose, wait, serialWrite, safeMode, passiveMode, programSong, playSong} from './index'

const B = 71
const E = 71 + 4
const F = 71 + 5
const G = 71 + 7
const Gs = 71 + 8

const quarterNote = 1000 / 4

const song1Notes = [B,E,B,G,B,E,B,G,B,E,B,G,B,E,B,G]
const song2Notes = [B,F,B,Gs,B,F,B,Gs,B,F,B,Gs,B,F,B,Gs]

serialOpen()
  .then(() => wait(1000))
  .then(() => safeMode())
  .then(() => wait(1000))
  .then(() => programSong(0, song1Notes, Array(song1Notes.length).fill(16)))
  .then(() => wait(1000))
  .then(() => programSong(1, song2Notes, Array(song2Notes.length).fill(16)))
  .then(() => wait(1000))
  .then(() => playSong(0))
  .then(() => wait(quarterNote * song1Notes.length + 10))
  .then(() => playSong(1))
  .then(() => wait(quarterNote * song2Notes.length + 10))
  .then(() => passiveMode())
  .then(() => wait(1000))
  .then(() => serialClose())
```

Movement Example:
```js
import {serialOpen, serialClose, wait, safeMode, moveForward, stopMotion, turnClockwise} from './index'

serialOpen()
  .then(() => wait(1000))
  .then(() => safeMode())
  .then(() => wait(1000))
  .then(() => moveForward(100))
  .then(() => wait(1000))
  .then(() => stopMotion())
  .then(() => turnClockwise())
  .then(() => wait(1500))
  .then(() => stopMotion())
  .then(() => wait(1000))
  .then(() => moveForward(100))
  .then(() => wait(1000))
  .then(() => stopMotion())
  .then(() => wait(1000))
  .then(() => serialClose())
  .catch(e => console.error(e.stack))
  .then(() => serialClose())
```
