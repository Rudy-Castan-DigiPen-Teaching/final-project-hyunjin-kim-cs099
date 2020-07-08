**1. Shapes**  
I used Shapes for Googly, Black thing which rise upside, every platforms.  
  
Code for making platform design:  
``` 
    push();
    noStroke();
    fill('#4e9c3b');
    rect(this.x, this.y, this.w, 13.75, 5, 5, 0, 0);
    fill('#946335');
    beginShape();
    vertex(this.x, this.y + 12.75);
    for (let i = 5; i <= this.w - 5; i += 15) {
      vertex(this.x + i, this.y + 5 + 13.75 / 2 + 30 * sin(i / this.w * PI) + underplatY[i] * 1.5);
    }
    vertex(this.x + this.w, this.y + 12.75);
    endShape(CLOSE);
    pop();  
```
    
**2. Colors**  
I used Colors for Googly's color.  
  
Code for use Color:  
```
  var Slider = {
    ColorPicker: null,
    BGM: null,
    SFX: null
  }

    Slider.colorPicker = createColorPicker(googly.color);
    googly.color = Slider.colorPicker.color();
    
    push();
    noStroke();
    fill(googly.color);
    translate(x, y);
    beginShape();
    var xoff = 0;
    for (let i = 0; i < TWO_PI; i += 0.1) {
      let n = map(noise(xoff, yoff), 0, 1, -2.3, 2.3);
      let hei = map(this.vel.y, -10, 10, this.r, this.r * 3) + n;
      let wid = map(this.vel.y, -10, 10, this.r * 3, this.r) + n;
      hei = constrain(hei, 15, 40);
      wid = constrain(wid, 15, 25);
      let x = wid * sin(i);
      let y = hei * cos(i);
      vertex(x, y);
      xoff += 0.1;
    }
    endShape(CLOSE);
    yoff += 0.06;
    pop();
```  

**3. Variables**

**4. Conditional Statements**

**5. Loops**

**6. Functions**

**7. Classes**

**8. Arrays**
