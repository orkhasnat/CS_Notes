``` html
<!DOCTYPE html>
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->
<html>
    <head>
        <title>water.click</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <style>
            body
            {
                background-color: #000000;
                font-family: sans-serif;
                color: #333333;
                font-size: 12px;
            }

            h1
            {
                font-family: sans-serif;
                color: #333333;
                font-size: 50px;
            }
        </style>
    </head>
    <body>
    <center>
        <br><br><br>
        <canvas id ="tint" width ="1000" height ="500"></canvas>
    </center>
    <script>
        var canvas = document.getElementById('tint');
        var ctx = canvas.getContext('2d');
        //var lvl = 1;
        ctx.fillStyle = '#FFFFFF';
        var plus = 0;
        var mouseX = 0;
        var mouseY = 0;
                //    var boxX = 0;
            //var boxY = 0;
            //var boxSize = 0;
        //var clicked = false;
         //var sqWidth = 0;
         //var difficulty = 0;
         //var box;
         //var color = getRandColor();
         setInterval(draw, 50);
        // setInterval(function(){ tint = 0; }, 18);
        // var tint = 0;
         var effect = 0;
         var eX = 0;
         var eY = 0;
         var distanceX = 0;
         var distanceY = 0;
         
                    canvas.addEventListener('click', function (evt) {
                       var rect = canvas.getBoundingClientRect();
            mouseY = evt.clientY - rect.top;
            mouseX = evt.clientX - rect.left;
            }
        );
        //var temp = 0;
        function draw() {

            var count = 0;
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            size = 5;
            //var number = 100+p/100;
            var p = 10;
            var d = 0;
            //ctx.fillRect(0, 0, 500, 500);
            
           if(effect > 0){
               effect = effect - 1;
           }
           else if(mouseX > 0 && mouseY > 0 && effect == 0){
                   effect = 20;
                   eX = mouseX;
                   eY = mouseY;
                   mouseX = 0;
                   mouseY = 0;
           }
         
            for (var y = p + size; y <= canvas.height - size/2; y += size + p) {
                for (var x = p + size + Math.cos(plus); x <= canvas.width - size/2; x += size + p, count += 1) {
                    
                    var a= (eX-x);
                   var b = eY - y;
                   d = Math.sqrt((a*a)+(b*b));

                ctx.beginPath();
                var dX = x/d;
                var dY = y/d;
                ctx.arc(x + Math.cos(plus)*(6+(dX*effect)), y + Math.sin(plus)*(2+(dX*effect)), 1, 0, 2*Math.PI);
                    ctx.fill();
                    plus += Math.PI/16;

                }


//                 //plus = plus + .000005;
                 
                 
            }
           
        }

        function getMouseX(canvas, event){
            var rect = canvas.getBoundingClientRect();
            var x = event.clientX - rect.left;
            return x;
        }
        
        function getMouseX(canvas, event){
            var rect = canvas.getBoundingClientRect();
            var y = event.clientY - rect.top;
            return y;
        }


//        function lighten(color, luminosity) {
//
//            // validate hex string
//            color = new String(color).replace(/[^0-9a-f]/gi, '');
//            if (color.length < 6) {
//                color = color[0] + color[0] + color[1] + color[1] + color[2] + color[2];
//            }
//            luminosity = luminosity || 0;
//
//            // convert to decimal and change luminosity
//            var newColor = "#", c, i, black = 0, white = 255;
//            for (i = 0; i < 3; i++) {
//                c = parseInt(color.substr(i * 2, 2), 16);
//                c = Math.round(Math.min(Math.max(black, c + (luminosity * white)), white)).toString(16);
//                newColor += ("00" + c).substr(c.length);
//            }
//            return newColor;
//        }
//        function getRandColor() {
//            var letters = '0123456789ABCDEF'.split('');
//            var color = '#';
//            for (var i = 0; i < 6; i++) {
//                color += letters[Math.floor(Math.random() * 16)];
//            }
//            return color;
//        }
    </script>
</body>
</html>

```