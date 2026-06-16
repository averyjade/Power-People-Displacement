---
order: 3
---
```js
function createFloodSystem() {

  // remove any previous flood canvas (prevents stacking)
  document.querySelectorAll("canvas[data-flood='true']").forEach(c => c.remove());

  const canvas = document.createElement("canvas");
  const ctx = canvas.getContext("2d");

  canvas.dataset.flood = "true";

  canvas.style.position = "fixed";
  canvas.style.left = "0";
  canvas.style.top = "0";
  canvas.style.width = "100vw";
  canvas.style.height = "100vh";
  canvas.style.pointerEvents = "none";
  canvas.style.zIndex = "5";

  document.body.appendChild(canvas);

  let w = canvas.width = window.innerWidth * devicePixelRatio;
  let h = canvas.height = window.innerHeight * devicePixelRatio;
  ctx.scale(devicePixelRatio, devicePixelRatio);

  let flood = parseFloat(sessionStorage.getItem("flood") || "0");
  let target = flood;

  const color = "rgba(10, 136, 207, 0.35)";

  function draw() {
    ctx.clearRect(0, 0, window.innerWidth, window.innerHeight);

    const time = performance.now() * 0.001;
    const wave = Math.sin(time * 1.2) * 0.03;

    const level = flood + wave;

    const y = window.innerHeight - level * (window.innerHeight + 120);

    ctx.fillStyle = color;
    ctx.beginPath();
    ctx.moveTo(0, window.innerHeight);
    ctx.lineTo(0, y);
    ctx.lineTo(window.innerWidth, y);
    ctx.lineTo(window.innerWidth, window.innerHeight);
    ctx.closePath();
    ctx.fill();

    // smooth movement only (NO transition states)
    flood += (target - flood) * 0.05;

    sessionStorage.setItem("flood", target);

    requestAnimationFrame(draw);
  }

  draw();

  function setLevel(v) {
    target = v;
    sessionStorage.setItem("flood", v);
  }

  return { setLevel };
}
```

<link rel="stylesheet" href="/style.css">

<div class="global-banner">
  <div class="global-banner__track">
    Flooding is not an event. &nbsp;&nbsp;
    It is a process of gradual displacement. &nbsp;&nbsp;
    What becomes visible is not the water itself, but what it replaces. &nbsp;&nbsp;
  </div>
</div>

# The Messaure Power Plant

Constructed on the Greater Lule River between the 1950s and 1960s, the Messaure project further consolidated the destruction of Sámi infrastructure.

Livelihood Destruction: The reservoir directly impacted several samebyar (Sámi reindeer herding districts), most notably the Slakka Sámi village, which relied on the valley as year-round pasture.
Submerged History: Cultural surveys conducted just prior to flooding revealed three highly significant Stone Age settlements and extensive ancient trapping pit systems used by ancestral Sámi to hunt wild reindeer. These historical records were drowned permanently under the reservoir.

Loss of Homesteads: Over 54 properties were affected, including long-established crown crofts like Njuoravuolle, marked on the map below, displacing families who relied on the river ecosystem.

```js
const floodSystem = createFloodSystem();
```
```js
floodSystem.setLevel(0.65);
```

- [Continue → Map 2](./05-map-2)