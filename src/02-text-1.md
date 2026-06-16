---
order: 1
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

# The Suorva Dam and Akkajaure Reservoir

The Suorva Dam and Akkajaure Reservoir
The construction of the Suorva Dam, which began in 1919 within what was then Stora Sjöfallet National Park, is widely regarded as one of the most devastating interventions for two major reasons:

The Flooding: To feed the dam, the state created the massive Akkajaure artificial reservoir. The rising waters completely swallowed whole valleys, ancient Sámi seasonal settlements, and centuries-old burial grounds. In the modern day, there is no safe way to cross this reservoir without boats or helicopters, neither of which the Sámi traditionally use.
Destruction of a Natural Wonder: This project also permanently silenced the Stora Sjöfallet waterfall (once known as the "Niagara of the North") and effectively turned a protected national park into an industrial hub.

```js
const floodSystem = createFloodSystem();
```

```js
floodSystem.setLevel(0.30);
```

- [Continue → Map 1](./03-map-1)
