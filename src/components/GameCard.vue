<template>
  <div class="game">
    
    <header class="wrap">
      <!-- <h1>Snake</h1> -->
      <div style="display:flex; flex-direction:column; align-items: center; margin: 0px auto;" class="score">
        <img style="margin-bottom:20px" width="60%" src="../assets/score.svg" alt="">
        <img width="30px" style="margin-bottom:20px" height="30px" id="score_value" src="../assets/0.svg"></div>
    </header>
    <canvas class="wrap" id="snake" width="320" height="320" tabindex="1"></canvas>

    <!-- Game Over Screen -->
    <div id="gameover">
      <img width="50%"  src="../assets/loadens.svg" alt="">
      <br>
      <img width="150%" src="../assets/wdywb.svg" alt="">
     
      <input style="width: 250px" type="text">
      
      <!-- <p>press <span style="background-color: #FFFFFF; color: #000000">space</span> to begin</p> -->
      <img id="newgame_gameover" src="../assets/new-game.svg" alt="">
      <img src="../assets/setings.svg"  id="setting_gameover"/>
    </div>

    <!-- Setting screen -->
    <div id="setting">
      <!-- <img width="60%" src="../assets/setings.svg" alt="" style="margin-bottom:10px"> -->
      
      <img width="90%" style="margin-bottom:10%" id="newgame_setting" src="../assets/new-game.svg">

         <img width="60%" src="../assets/speed.svg" alt="">
      <div>
        <input id="speed1" type="radio" name="speed" value="120" checked />
        <label for="speed1">
          <img width="30%" src="../assets/slow_подсветка.svg" alt="">
        </label>
        <input id="speed2" type="radio" name="speed" value="75" />
        <label for="speed2">
          <img width="30%" src="../assets/normal.svg" alt="">
        </label>
        <input id="speed3" type="radio" name="speed" value="35" />
        <label for="speed3">
          <img width="30%" src="../assets/fast.svg" alt="">
        </label>
      </div>

        <img width="60%" src="../assets/wall.svg" alt="">
      <div>

        <input id="wallon" type="radio" name="wall" value="1" checked />
        <label for="wallon">
          <img width="20%" src="../assets/on.svg" alt="">
        </label>
        <input id="walloff" type="radio" name="wall" value="0" />
        <label for="walloff">
          <img width="20%" src="../assets/off.svg" alt="">
        </label>
      </div>

    </div>

    <!-- Main Menu Screen -->
    <div id="menu">
       <img width="60%" src="../assets/loadens.svg" alt="">

      <img width="60%" id="newgame_menu" src="../assets/new-game.svg">
      <img width="60%" src="../assets/setings.svg"  id="setting_menu">
    </div>

  </div>
</template>

<script>
export default {
  name: 'GameCard',
  props: {
    msg: String
  },
  data() {
    return {
       get score() {
        return localStorage.getItem('snakeScore') || 0;
      },
      set score(value) {
        localStorage.setItem('snakeScore', value);
      }
    }
  },
  // mounted() {
  //   /**
  //  * Snake game created with plain JavaScript by Ibrahim fariat.
  //  **/

  //   let dom_replay = document.querySelector("#replay");
  //   let dom_score = document.querySelector("#score");
  //   let dom_canvas = document.createElement("canvas");
  //   document.querySelector("#canvas").appendChild(dom_canvas);
  //   let CTX = dom_canvas.getContext("2d");

  //   const W = (dom_canvas.width = 300);
  //   const H = (dom_canvas.height = 300);

  //   let snake,
  //     food,
  //     currentHue,
  //     cells = 20,
  //     cellSize,
  //     isGameOver = false,
  //     // tails = [],
  //     score = 0,
  //     maxScore = window.localStorage.getItem("maxScore") || undefined,
  //     particles = [],
  //     splashingParticleCount = 20,
  //     // cellsCount,
  //     requestID;

  //   let helpers = {
  //     Vec: class {
  //       constructor(x, y) {
  //         this.x = x;
  //         this.y = y;
  //       }
  //       add(v) {
  //         this.x += v.x;
  //         this.y += v.y;
  //         return this;
  //       }
  //       mult(v) {
  //         if (v instanceof helpers.Vec) {
  //           this.x *= v.x;
  //           this.y *= v.y;
  //           return this;
  //         } else {
  //           this.x *= v;
  //           this.y *= v;
  //           return this;
  //         }
  //       }
  //     },
  //     isCollision(v1, v2) {
  //       return v1.x == v2.x && v1.y == v2.y;
  //     },
  //     garbageCollector() {
  //       for (let i = 0; i < particles.length; i++) {
  //         if (particles[i].size <= 0) {
  //           particles.splice(i, 1);
  //         }
  //       }
  //     },
  //     drawGrid() {
  //       CTX.lineWidth = 1.1;
  //       CTX.strokeStyle = "#232332";
  //       CTX.shadowBlur = 0;
  //       // for (let i = 1; i < cells; i++) {
  //       //   let f = (W / cells) * i;
  //       //   CTX.beginPath();
  //       //   CTX.moveTo(f, 0);
  //       //   CTX.lineTo(f, H);
  //       //   CTX.stroke();
  //       //   CTX.beginPath();
  //       //   CTX.moveTo(0, f);
  //       //   CTX.lineTo(W, f);
  //       //   CTX.stroke();
  //       //   CTX.closePath();
  //       // }
  //     },
  //     randHue() {
  //       return ~~(Math.random() * 360);
  //     },
  //     hsl2rgb(hue, saturation, lightness) {
  //       if (hue == undefined) {
  //         return [0, 0, 0];
  //       }
  //       let chroma = (1 - Math.abs(2 * lightness - 1)) * saturation;
  //       let huePrime = hue / 60;
  //       let secondComponent = chroma * (1 - Math.abs((huePrime % 2) - 1));

  //       huePrime = ~~huePrime;
  //       let red;
  //       let green;
  //       let blue;

  //       if (huePrime === 0) {
  //         red = chroma;
  //         green = secondComponent;
  //         blue = 0;
  //       } else if (huePrime === 1) {
  //         red = secondComponent;
  //         green = chroma;
  //         blue = 0;
  //       } else if (huePrime === 2) {
  //         red = 0;
  //         green = chroma;
  //         blue = secondComponent;
  //       } else if (huePrime === 3) {
  //         red = 0;
  //         green = secondComponent;
  //         blue = chroma;
  //       } else if (huePrime === 4) {
  //         red = secondComponent;
  //         green = 0;
  //         blue = chroma;
  //       } else if (huePrime === 5) {
  //         red = chroma;
  //         green = 0;
  //         blue = secondComponent;
  //       }

  //       let lightnessAdjustment = lightness - chroma / 2;
  //       red += lightnessAdjustment;
  //       green += lightnessAdjustment;
  //       blue += lightnessAdjustment;

  //       return [
  //         Math.round(red * 255),
  //         Math.round(green * 255),
  //         Math.round(blue * 255)
  //       ];
  //     },
  //     lerp(start, end, t) {
  //       return start * (1 - t) + end * t;
  //     }
  //   };

  //   let KEY = {
  //     ArrowUp: false,
  //     ArrowRight: false,
  //     ArrowDown: false,
  //     ArrowLeft: false,
  //     resetState() {
  //       this.ArrowUp = false;
  //       this.ArrowRight = false;
  //       this.ArrowDown = false;
  //       this.ArrowLeft = false;
  //     },
  //     listen() {
  //       addEventListener(
  //         "keydown",
  //         (e) => {
  //           if (e.key === "ArrowUp" && this.ArrowDown) return;
  //           if (e.key === "ArrowDown" && this.ArrowUp) return;
  //           if (e.key === "ArrowLeft" && this.ArrowRight) return;
  //           if (e.key === "ArrowRight" && this.ArrowLeft) return;
  //           this[e.key] = true;
  //           Object.keys(this)
  //             .filter((f) => f !== e.key && f !== "listen" && f !== "resetState")
  //             .forEach((k) => {
  //               this[k] = false;
  //             });
  //         },
  //         false
  //       );
  //     }
  //   };

  //   class Snake {
  //     constructor(i, type) {
  //       this.pos = new helpers.Vec(W / 2, H / 2);
  //       this.dir = new helpers.Vec(0, 0);
  //       this.type = type;
  //       this.index = i;
  //       this.delay = 5;
  //       this.size = W / cells;
  //       this.color = "black";
  //       this.history = [];
  //       this.total = 1;
  //     }
  //     draw() {
  //       let { x, y } = this.pos;
  //       CTX.fillStyle = this.color;
  //       CTX.shadowBlur = 20;
  //       CTX.shadowColor = "rgba(255,255,255,.3 )";
  //       CTX.fillRect(x, y, this.size, this.size);
  //       CTX.shadowBlur = 0;
  //       if (this.total >= 2) {
  //         for (let i = 0; i < this.history.length - 1; i++) {
  //           let { x, y } = this.history[i];
  //           CTX.lineWidth = 1;
  //           CTX.fillStyle = "black";
  //           CTX.fillRect(x, y, this.size, this.size);
  //         }
  //       }
  //     }
  //     walls() {
  //       let { x, y } = this.pos;
  //       if (x + cellSize > W) {
  //         this.pos.x = 0;
  //       }
  //       if (y + cellSize > W) {
  //         this.pos.y = 0;
  //       }
  //       if (y < 0) {
  //         this.pos.y = H - cellSize;
  //       }
  //       if (x < 0) {
  //         this.pos.x = W - cellSize;
  //       }
  //     }
  //     controlls() {
  //       let dir = this.size;
  //       if (KEY.ArrowUp) {
  //         this.dir = new helpers.Vec(0, -dir);
  //       }
  //       if (KEY.ArrowDown) {
  //         this.dir = new helpers.Vec(0, dir);
  //       }
  //       if (KEY.ArrowLeft) {
  //         this.dir = new helpers.Vec(-dir, 0);
  //       }
  //       if (KEY.ArrowRight) {
  //         this.dir = new helpers.Vec(dir, 0);
  //       }
  //     }
  //     selfCollision() {
  //       for (let i = 0; i < this.history.length; i++) {
  //         let p = this.history[i];
  //         if (helpers.isCollision(this.pos, p)) {
  //           isGameOver = true;
  //         }
  //       }
  //     }
  //     update() {
  //       // console.log(1)
  //       this.walls();
  //       this.draw();
  //       this.controlls();
  //       if (!this.delay--) {
  //         if (helpers.isCollision(this.pos, food.pos)) {
  //           incrementScore();
  //           particleSplash();
  //           food.spawn();
  //           this.total++;
            
            
  //         }
  //         this.history[this.total - 1] = new helpers.Vec(this.pos.x, this.pos.y);
  //         for (let i = 0; i < this.total - 1; i++) {
  //           this.history[i] = this.history[i + 1];
  //         }
  //         this.pos.add(this.dir);
  //         this.delay = 5;
  //         this.total > 3 ? this.selfCollision() : null;
  //       }
  //     }
  //   }

  //   class Food {
  //     constructor() {
  //       this.pos = new helpers.Vec(
  //         ~~(Math.random() * cells) * cellSize,
  //         ~~(Math.random() * cells) * cellSize
  //       );
  //       this.color = currentHue = `hsl(${~~(Math.random() * 360)},100%,50%)`;
  //       this.size = cellSize;
  //     }
  //     draw() {
  //       let { x, y } = this.pos;
  //       CTX.globalCompositeOperation = "lighter";
  //       CTX.shadowBlur = 20;
  //       CTX.shadowColor = this.color;
  //       CTX.fillStyle = this.color;
  //       CTX.fillRect(x, y, this.size, this.size);
  //       CTX.globalCompositeOperation = "source-over";
  //       CTX.shadowBlur = 0;
  //     }
  //     spawn() {
  //       let randX = ~~(Math.random() * cells) * this.size;
  //       let randY = ~~(Math.random() * cells) * this.size;
  //       for (let path of snake.history) {
  //         if (helpers.isCollision(new helpers.Vec(randX, randY), path)) {
  //           return this.spawn();
  //         }
  //       }
  //       this.color = currentHue = `hsl(${helpers.randHue()}, 100%, 50%)`;
  //       this.pos = new helpers.Vec(randX, randY);
  //     }
  //   }

  //   class Particle {
  //     constructor(pos, color, size, vel) {
  //       this.pos = pos;
  //       this.color = color;
  //       this.size = Math.abs(size / 2);
  //       this.ttl = 0;
  //       this.gravity = -0.2;
  //       this.vel = vel;
  //     }
  //     draw() {
  //       let { x, y } = this.pos;
  //       let hsl = this.color
  //         .split("")
  //         .filter((l) => l.match(/[^hsl()$% ]/g))
  //         .join("")
  //         .split(",")
  //         .map((n) => +n);
  //       let [r, g, b] = helpers.hsl2rgb(hsl[0], hsl[1] / 100, hsl[2] / 100);
  //       CTX.shadowColor = `rgb(${r},${g},${b},${1})`;
  //       CTX.shadowBlur = 0;
  //       CTX.globalCompositeOperation = "lighter";
  //       CTX.fillStyle = `rgb(${r},${g},${b},${1})`;
  //       CTX.fillRect(x, y, this.size, this.size);
  //       CTX.globalCompositeOperation = "source-over";
  //     }
  //     update() {
  //       this.draw();
  //       this.size -= 0.3;
  //       this.ttl += 1;
  //       this.pos.add(this.vel);
  //       this.vel.y -= this.gravity;
  //     }
  //   }
  //   function incrementScore() {
  //     score++;
  //     // that.score = score
  //     dom_score.innerText = score.toString().padStart(2, "0");
  //   }

  //   function particleSplash() {
  //     for (let i = 0; i < splashingParticleCount; i++) {
  //       let vel = new helpers.Vec(Math.random() * 6 - 3, Math.random() * 6 - 3);
  //       let position = new helpers.Vec(food.pos.x, food.pos.y);
  //       particles.push(new Particle(position, currentHue, food.size, vel));
  //     }
  //   }

  //   function clear() {
  //     CTX.clearRect(0, 0, W, H);
  //   }

  //   function initialize() {
  //     CTX.imageSmoothingEnabled = false;
  //     KEY.listen();
  //     // cellsCount = cells * cells;
  //     cellSize = W / cells;
  //     snake = new Snake();
  //     food = new Food();
  //     dom_replay.addEventListener("click", reset, false);
  //     loop();
  //   }

  //   function loop() {
  //     clear();
  //     if (!isGameOver) {
  //       requestID = setTimeout(loop, 1000 / 60);
  //       helpers.drawGrid();
  //       snake.update();
  //       food.draw();
  //       for (let p of particles) {
  //         p.update();
  //       }
  //       helpers.garbageCollector();
  //     } else {
  //       clear();
  //       gameOver();
  //     }
  //   }

  //   function gameOver() {
  //     maxScore ? null : (maxScore = score);
  //     score > maxScore ? (maxScore = score) : null;
      
  //     window.localStorage.setItem("snakeScore", score);
  //     window.localStorage.setItem("maxScore", maxScore);
  //     CTX.fillStyle = "#4cffd7";
  //     CTX.textAlign = "center";
  //     CTX.font = "bold 30px Poppins, sans-serif";
  //     CTX.fillText("GAME OVER", W / 2, H / 2);
  //     CTX.font = "15px Poppins, sans-serif";
  //     CTX.fillText(`SCORE   ${score}`, W / 2, H / 2 + 60);
  //     CTX.fillText(`MAXSCORE   ${maxScore}`, W / 2, H / 2 + 80);
  //   }

  //   function reset() {
  //     dom_score.innerText = "00";
  //     score = "00";
  //     snake = new Snake();
  //     food.spawn();
  //     KEY.resetState();
  //     isGameOver = false;
  //     clearTimeout(requestID);
  //     loop();
  //   }

  //   initialize();

  // }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  font-size: 20px;
  color: black;
  background-color: rgb(165,202,109);
  padding: 10px;
  border: 2px solid black;
  outline: none;
  font-family: 'Arial';
  border-radius: 20px;
  height: 50px;
}
img{ 
  cursor: pointer;
}
img:hover{
  /* transform: scale(1.1); */
}
.game{
  position: fixed;
top: 55%;
left: 50%;
transform: translate(-50%, -55%);

}
@import url("https://fonts.googleapis.com/css?family=VT323");

::selection {
  color: #FFFFFF;
  background: transparent;
}

::-moz-selection {
  color: #FFFFFF;
  background: transparent;
}

* {
  margin: 0;
  padding: 0;
  font-family: "VT323";
}

body {
  background-color: #000000;
}

.wrap {
  margin-left: auto;
  margin-right: auto;
}

header {
  width: 340px;
  font-size: 0;
}

canvas {
  display: none;
  border-style: solid;
  border-width: 10px;
  border-color: #FFFFFF;
}

canvas:focus {
  outline: none;
}

/* Top Styles */
h1 {
  display: inline-block;
  width: 100px;
  font-size: 32px;
  color: #FFFFFF;
}

.score {
  display: inline-block;
  width: 240px;
  font-size: 20px;
  color: #FFFFFF;
  text-align: right;
}

.score_value {
  font-size: inherit;
}



/* All screens style */
#gameover a,
#setting a,
#menu a {
  display: block;
}

#gameover a,
#setting a:hover,
#menu a:hover {
  cursor: pointer;
}

#gameover a:hover::before,
#setting a:hover::before,
#menu a:hover::before {
  /* content: ">"; */
  margin-right: 10px;
}

/* Menu Screen Style */
#menu {
  display: block;
  width: 340px;
  /* padding-top: 95px; */
  padding-bottom: 95px;
  font-size: 40px;
  margin-left: auto;
  margin-right: auto;
  text-align: center;
  color: #FFF;
}

#menu img:first-child {
  -webkit-animation: logo-ani 1000ms linear infinite;
  animation: logo-ani 1000ms linear infinite;
  margin-bottom: 30px;

}

#menu a {
  font-size: 30px;
}

@-webkit-keyframes logo-ani {
  50% {
    -webkit-transform: scale(1.3, 1.3);
  }

  100% {
    -webkit-transform: scale(1.0, 1.0);
  }
}

@keyframes logo-ani {
  50% {
    transform: scale(1.3, 1.3);
  }

  100% {
    transform: scale(1.0, 1.0);
  }
}


/* Game Over Screen Style */

#gameover {
  display: none;
  width: 340px;
  /* padding-top: 95px; */
  padding-bottom: 95px;
  margin-left: auto;
  margin-right: auto;
  text-align: center;
  font-size: 30px;
  color: #FFF;
}

#gameover p {
  margin-top: 25px;
  font-size: 20px;
}

/* Settings Screen Style */
#setting {
  display: none;
  width: 340px;
  margin-left: auto;
  margin-right: auto;
  /* padding-top: 85px; */
  padding-bottom: 85px;
  font-size: 30px;
  color: #FFF;
  text-align: center;
}

#setting h2 {
  margin-bottom: 15px;
}

#setting p {
  margin-top: 10px;
}

#setting input {
  display: none;
}

#setting label {
  cursor: pointer;
}

#setting input:checked+label {
  background-color: #fff;
  /* background-color: #FFF;
  color: #000; */
}
</style>
