var w = innerWidth, h = innerHeight;
var v = Math.min(w, h), cvs, ctx;

onload = function() {
  cvs = document.querySelector("canvas");
  cvs.width = w; cvs.height = h;
  ctx = cvs.getContext("2d");
  
  animate();
}

function animate() {
  var t = Date.now() / 2000;
  
  ctx.fillStyle = "rgba(0, 0, 0, 0.05)";
  ctx.fillRect(0, 0, w, h);
  
  for(var k = 0; k <4; k++) {
    var angleK = 2*Math.PI * k/4 + Math.PI/4 + t/5;
    var startX = w/2 + v/3 * Math.cos(angleK);
    var startY = h/2 + v/3 * Math.sin(angleK);
    
    for (var i = 0; i < 6; i++) {
      var angle = 2*Math.PI * i/6 - t;
      var R = v / 8, r = v / 75;
      
      var x = startX + R * Math.cos(angle);
      var y = startY + R * Math.sin(angle);
      
      for (var j = 0; j < 6; j++) {
        var angle2 = 2*Math.PI * j/6 * Math.sin(t/2) + angle - 3 * t;
        
        var x2 = x + 8*r * Math.cos(angle2);
        var y2 = y + 8*r * Math.sin(angle2);
        
        ctx.beginPath();
        ctx.arc(x2, y2, r/2, 0, 2*Math.PI);
        ctx.fillStyle = 'hsl(${6*angle + Math.PI/2}rad, 50%, 50%)';
        ctx.fill();
      }
      
      ctx.beginPath();
      ctx.arc(x, y, r, 0, 2*Math.PI);
      ctx.fillStyle = 'hsl(${6*angle}rad, 50%, 50%)';
      ctx.fill();
    }
  }
  
  requestAnimationFrame(animate);
}
