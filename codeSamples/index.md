---
layout: default
title:  "Code Samples"
---


<div class="col-md-6" id="sieve-of-eratosthenes">



<button id="click-me-button" type="button" onclick="startSieve()">
   sieve numbers
</button>
<input id="sieve-parameter" type="number">

</div>

```scala
def sieveOfEratosthenes(n: Int): Int = {
    val m = n + 1
    val maxRoot: Int = 
	math.sqrt(m).floor.asInstanceOf[Int]
    val notPrime =
	Array.fill[Boolean](m)(false)
    notPrime(0) = true // 0 not prime
    notPrime(1) = true // 1 not prime

    for (i <- 2 to maxRoot) {
      var k = 2
      var product: Int = i*k
      while (product < m) {
        notPrime(product) = true
        k += 1
        product = i*k
      }
    }

    notPrime.count(p => !p)
}
```

<!--
<div id="banner-gen">
<button id="ban-gen-button" type="button" onclick="generateBanner()">
    generate banner
</button>
<input id="banner-parameter" type="text">
</div>
-->

<!-- Include JavaScript dependencies -->
<script type="text/javascript" src="setupscalajs-jsdeps.js"></script>
<!-- Include your source -->
<script type="text/javascript" src="setupscalajs-fastopt.js"></script>

<div class="col-md-12" id="goldenRatioGradientMixer">
<br>
<h1>Golden ratio color gradient mixer</h1>
<!-- This calls a function from an object in the source, so it is below the source import -->
<canvas id="canvas" height="350px" width ="550px">
</canvas>

<p>Red amount:</p>
<input type="range" id="r-val-incr" value="10" onchange="canvasFibonacci.Canvas().redIncr">

<p>Green amount:</p>
<input type="range" id="g-val-incr" value="10" onchange="canvasFibonacci.Canvas().greenIncr">

<p>Blue amount:</p> 
<input type="range" id="b-val-incr" value="10" onchange="canvasFibonacci.Canvas().blueIncr">

<script>
    canvasFibonacci.Canvas().main(document.getElementById('canvas'));
</script>
</div>

```scala
    def run: Unit = {
        if(counter >= numBoxes){
          fill("#C8C8E6")
          counter = 0
          initPrevCorners()
        }

        val sideLength = k*(1 / math.pow(phi, counter)).toFloat

        counter%4 match {
          case 0 => // move up/start
            startCorner = Point(
              previousCorners(1).x,
              previousCorners(1).y - sideLength
            )
          case 1 => // move right
            startCorner = Point(
              previousCorners(2).x,
              previousCorners(2).y
            )
          case 2 => // move down
            startCorner = Point(
              previousCorners(3).x - sideLength,
              previousCorners(3).y
            )
          case 3 => // move left
            startCorner = Point(
              previousCorners(0).x - sideLength,
              previousCorners(0).y - sideLength
            )
        }

        ctx.fillStyle = s"rgb($rVal, $gVal, $bVal)"
        rVal += rValIncr
        bVal += bValIncr
        gVal += gValIncr
        if(rVal > 255 || gVal > 255 || bVal > 255){
          rVal = 5
          bVal = 5
          gVal = 5
        }

        ctx.fillRect(startCorner.x, startCorner.y, sideLength, sideLength)
        updatePrevCorners(sideLength)

        counter += 1
        if(counter < numBoxes)
          dom.window.setTimeout(() => run, 50)
        else
          dom.window.setTimeout(() => run, 5000)
      }

    dom.window.onload = { (e: Event) => run }
```
