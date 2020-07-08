`// let player = Googly;`  
  
  
    
**1. Shapes**  
I used Shapes for Googly, Black thing which rise upside, every platforms.  
  
Code for making platform design:  
``` 
    beginShape();
    vertex(this.x, this.y + 12.75);
    for (let i = 5; i <= this.w - 5; i += 15) {
      vertex(this.x + i, this.y + 5 + 13.75 / 2 + 30 * sin(i / this.w * PI) + underplatY[i] * 1.5);
    }
    vertex(this.x + this.w, this.y + 12.75);
    endShape(CLOSE);
```
    
**2. Colors**  
I used Colors for Googly's color.  
  
Code for Googly preview in option:  
```
  let yoff = 0;
  var Slider = {
    ColorPicker: null
  }

  Slider.colorPicker = createColorPicker(googly.color);
  googly.color = Slider.colorPicker.color();

  for (let j = 0; j < 2; j++) {
    push();
    noStroke();
    fill(googly.color);
    translate(600 + j * 110, height * 0.765);
    beginShape();
    var xoff = 0;
    for (let i = 0; i < TWO_PI; i += 0.1) {
      let n = map(noise(xoff, yoff), 0, 1, -2.3, 2.3);
      let x = n + 23 * sin(i);
      let y = n + 23 * cos(i);
      vertex(x, y);
      xoff += 0.1;
    }
    endShape(CLOSE);
    yoff += 0.03;
    pop();
  }
```  

**3. Variables**  
Usually used JSON variables, to classify each variables.

Code for variables:
```
  let InScenes = { // variables related to Scenes
    nowScene: 'mainMenu',
    selected: 1,
    selectBoxY: 495,
    buttonY: 495,
    mainAlpha: 0,
    exitTime: 150,
    seeVoid: 400,
    over: 80,
  }
  
  let googly = { // variables for consisting Googly
    JumpCount: 2,
    dodged: false,
    IsStumping: false,
    canMove: true,
    state: 'air',
    lookat: 'for',
    eye: 'oo',
    eyepos: 0,
    stopped: 50,
    color: 'skyblue',
  }
```

**4. Conditional Statements**  
Most events required conditional statements.  
I used it for changing scenes, controlling Googly, selecting buttons, etc.  
  
Code for controlling Googly:
```
function keyPressed() {
  if ((InScenes.nowScene == 'gameStart' || InScenes.nowScene == 'tutorial') && googly.canMove == true) {
    if ((googly.state == 'ground' || googly.JumpCount > 0) && keyCode == 32) {
      Sound.jump.play();
      googly.JumpCount -= 1;
      googly.state = 'air';
      var aa = createVector(0, -5);
      player.getForce(aa);
      //console.log('jump');
    }

    if (googly.IsStumping == false && keyCode == 32 && keyIsDown(83)) {
      var stump = createVector(0, 15);
      player.getForce(stump);
      googly.IsStumping = true;
      //console.log(0);
    }
   }
  }
```

**5. Loops**  
I used `for loop` a lot by making dark thing, setting platforms' position, making Googly's flutter body, etc.
  
Code for setting platforms' position:
```
  platforms.push(new Box(-width * 3, height - 30, width * 6, 600));

  for (let i = -1; i < NofPlatforms; i++) {
    platform = new Box(random(-width, width), random(-2000 - (World.level * 800), height - 100), floor(random(2, 5)) * 60, 25);
    var overlapping = false;
    for (let j = 0; j < platforms.length; j++) {
      var other = platforms[j];
      let xcheck = abs(platform.x - other.x) < platform.w;
      let ycheck = abs(platform.y - other.y) < 100;
      if (xcheck && ycheck) {
        overlapping = true;
        break;
      }
    }
    if (!overlapping) {
      platforms.push(platform);
    }
  }
```

**6. Functions**
I used functions for create/clear maps, checking goal's y position, initializing Scenes or game.  

Code for initialize game:
```
function clearMap() {
  platforms.splice(0, platforms.length);
  highestBox.splice(0, highestBox.length);
}

function checkHighest() {
  for (let i = 0; i < platforms.length; i++) {
    highestBox.push(abs(platforms[i].y));
  }
  World.highplat = max(highestBox);
}

function initializePlayerpos() {
  player.pos.x = 0;
  player.pos.y = height - 100;
  googly.stopped = 50;
  googly.canMove = true;
  InScenes.seeVoid = 400;
  holy.y = 1500;
}

function initializeGame() {
  clearMap();
  createMap();
  checkHighest();
  initializePlayerpos();
}
```

**7. Classes**  
I use class for objects which makes events itself/with certain objects.

Cod for making Black thing:
```
class Holy {
  constructor(y) {
    this.x = Camera.x;
    this.y = y;
    this.w = width;
    this.h = 3000;
  }

  update() {
    World.dieTime = constrain(World.dieTime, -10, 30);
    this.y -= 1 + (((World.level - 1) * 0.1));
    this.x = Camera.x;

    if (player.pos.y > this.y + 70) {
      World.dieTime -= 1;
    } else {
      World.dieTime = 50;
    }

    if (World.dieTime < 0) {
      InScenes.nowScene = 'gameOver';
    }
    if (World.dieTime == 0) {
      Music.end.play();
      Music.end.setLoop(true);
        }
  }

  show() {
    for (let i = 0; i < 50; i++) {
    push();
    noStroke();
    fill(42, 28, 43, i * 5);
    rect(this.x - this.w * 1.5, this.y + (i * 7), this.w*4, 1000);
    pop();
    }
  }
}
```

**8. Arrays**  
Arrays are best way to stack certain values.  
I used it for saving object's positions.  

Code for saving Googly's position and use into roll effect:
```
  let googlypos = [];

    if (googly.dodged == true) {
      googlypos.push([this.pos.x, this.pos.y]);
    }
    if (googly.dodged == false || googly.IsStumping == true) {
      googlypos.splice(0, googlypos.length);
    }

    if (googly.dodged == true) {
      push();
      noStroke();
      fill(255, 0, 0, 70);
      for (let i = googlypos.length; i > 0; i--) {
        this.dashVisual = googlypos.length - i;
        this.dashVisual = constrain(this.dashVisual, 0, 15);
        circle(googlypos[googlypos.length - i][0], googlypos[googlypos.length - i][1], this.dashVisual);
      }
      pop();
    }
```

