```
// let player = Googly;
```
  
  
    
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

**7. Classes**

**8. Arrays**
