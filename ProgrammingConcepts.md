**1. Shapes**  
I used Shapes for Googly, Black thing which rise upside, every platforms.  
  
Code for making platform design:  
``` push();
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

    //rect(this.x, this.y, this.w, this.h - 15);
    pop(); ```  
    
**2. Colors**

**3. Variables**

**4. Conditional Statements**

**5. Loops**

**6. Functions**

**7. Classes**

**8. Arrays**
