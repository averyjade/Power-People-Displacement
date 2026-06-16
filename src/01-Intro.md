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

# Intro / Brief


# How did we get here?

Sami country – known as Sápmi – stretches across the northern parts of Sweden, Norway and Finland, and Russia’s Kola Peninsula. The original settlement was even larger, but the indigenous Sami were gradually forced to give up land, first to farmers starting in the 1650s and later to industries. https://sweden.se/life/people/sami-in-sweden



## Power Supply Background

Hydroelectric dams account for nearly 45% of Sweden's power supply, and it is no surprise large swaths of land have been flooded into retaining reservoirs for this cause. However, the consequences of these floods is frequently overlooked.

# The Range of Impact and Implications
Over 80% of this hydroelectric power comes from the Sapmi region of northern Sweden, where the indigenous Sámi peoples live and herd reindeer. Unfortunately, many of these dams were put in place with little to no free and informed prior consent. Not only is the land and biodiversity that their culture thrives on put in danger in these scenarios, but their settlements and herding paths were frequently washed away entirely. In nearby Norway, facing similar concerns, the Water Resources and Energy Directorate emphasizes that many former grazing pastures are no longer even touched by herds, with reindeer forced to scatter into new areas, or overgraze the other pre-existing pastures. This not only causes ecological concerns but also further forces the uprooting of the Sámi peoples. Furthermore, natural lakes and frozen rivers have historically served as the safest migration paths for reindeer herds. The deeper, fluctuating water levels caused by hydropower operations result in unstable and unsafe ice conditions, making it nearly impossible for animals or land-based travelers like the Sámi to cross.

# The Project
To help portray this problem more exactly, our team set out to provide geotechnical data on a few major instances of this flooding's negative impacts. Below, you will find information on each in particular, alongside sliding scales of the water banks before and after dam construction. 

```js
const floodSystem = createFloodSystem();
```

```js
floodSystem.setLevel(0.15);
```

- [Continue →The Suorva Dam and Akkajaure Reservoir](./02-text-1)