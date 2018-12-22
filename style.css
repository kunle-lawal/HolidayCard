var dots = [];
(function () {
    var canvas = document.getElementById("canvas");
    var ctx = canvas.getContext("2d");
    var cw = canvas.width;
    var ch = canvas.height;
    var map_w = cw * 1.3;
    var map_h = ch * 1.3;

    //partciles on the screen//
    var offset = {
        speedx: 20,
        speedy: 20,
        maxSpeed: 10,
        offSetting: false,
        directionX: 0,
        directionY: 0,
    };

    //Here we will update the virtual player's position
    var vPlayer = {
        x: 0,
        y: 0,
        worldx: randNum(-map_w, map_w),
        worldy: randNum(-map_h, map_h),
        vx: 0,
        vy: 0,
        update: function () {
            this.x += this.vx;
            this.y += this.vy;
        }
    };

    //Random number Generator
    function randNum(min, max) {
        return Math.random() * (max - min) + min;
    }

    function randVal(x, y) {
        var rand = randNum(1, 3);
        if (rand < 2) {
            return y;
        } else {
            return x;
        }
    }

    //Getting elements by ID for UI/UX
    function GID(id) {
        return document.getElementById(id);
    }

    //Make a random color
    function randColor() {
        var letters = '0123456789ABCDEF'.split('');
        var color = '#';
        for (var i = 0; i < 6; i++) {
            color += letters[Math.floor(Math.random() * 16)];
        }
        return color;
    }

    //Get the distance between object1 and object2
    function return_distance(object1_x, object1_y, object2_x, object2_y) {
        var dx = object1_x - object2_x;
        var dy = object1_y - object2_y;
        var d = Math.sqrt(dx * dx + dy * dy);

        return d;
    }

    //Get the angle of object1 against object2
    function return_angle(object1_x, object1_y, object2_x, object2_y) {
        var dx = object1_x - object2_x;
        var dy = object1_y - object2_y;

        var angle = Math.atan2(dy, dx);
        return angle;
    }

    //check collision between 2 objects based on position. 
    function checkCollisionObjects(object1, objects) {
        for (var i = 0; i < objects.length; i++) {
            var obj = objects[i];
            var object1ToObject2 = return_distance(object1.x, object1.y, obj.x, obj.y);
            if (object1ToObject2 < (object1.r) + obj.r) {
                return true;
            }
        }
        return false;
    }

    //Get the mouse posision. 
    function getMousePos(canvas, evt) {
        var rect = canvas.getBoundingClientRect();
        return {
            x: (evt.clientX - rect.left) / (rect.right - rect.left) * canvas.width,
            y: (evt.clientY - rect.top) / (rect.bottom - rect.top) * canvas.height
        };
    }

    //On mouse movement move the canvas aswell. 
    document.addEventListener('mousemove', function (evt) {
        var mousePos = getMousePos(canvas, evt);
        vPlayer.x = mousePos.x;
        // vPlayer.y = mousePos.y;
        offset.directionX = -mousePos.x / 30;
        // offset.directionY = -mousePos.y / 30;
    }, false);

    //Request animation frame for rendering
    window.requestAnimFrame = (function () {
        return window.requestAnimationFrame ||
            window.webkitRequestAnimationFrame ||
            window.mozRequestAnimationFrame ||
            function (callback) {
                window.setTimeout(callback, 1000 / 60);
            };
    })();


    /* Start Snow script */
    dots = [];
    var dotsDropped = 0;
    //Push 10 dots into the array
    for (var i = 0; i < 2000; i++) {
        var rand_radius = randNum(1, 3);
        var color = "rgba(255, 255, 255, 1)";
        dots.push({
            single: true,
            x: randNum(-map_w, map_w),
            y: randNum(-map_h, 0),
            r: rand_radius,
            energy: 0,
            vx: randNum(-4, 4) / randNum(2, 7),
            vy: randNum(5, 50) / randNum(2, 7),
            pos: i,
            speed: 1,

            life: randNum(10, 100),
            lived: 1,
            dots_touched: 0,
            greed: randNum(randVal(-1, 0), 2),
            feeding: false,
            eat_dis: 100,
            alive: true,

            og_color: color,
            color: color,

            stroke: 0,
        });
    }

    large = 0;
    for (var x = 0; x < dots.length; x++) {
        if (dots[x].dots_touched > large) {
            large = dots[x].dots_touched;
            posk = x;
        }
    }


    function draw_dots(dot) {
        ctx.save();
        ctx.translate((offset.directionX), (offset.directionY));
        // clear the viewport
        //ctx.clearRect(-offset.directionX, -offset.directionY, cw,ch);
        var dis = return_distance(vPlayer.x, vPlayer.y, dot.x, dot.y);

        ctx.beginPath();
        ctx.arc(dot.x, dot.y, dot.r + 1, 0, (2 * Math.PI));
        ctx.fillStyle = dot.color;
        ctx.fill();
        ctx.restore();
    }


    // Logic for the dots 
    function update_dots() {
        for (var i = 0; i < dots.length; i++) {
            var dot = dots[i];
            dot.x += dot.vx;
            dot.y += dot.vy;

            var dis_to_center = return_distance(cw / 2, ch / 2, dot.x, dot.y);
            var ang = return_angle(vPlayer.x, vPlayer.y, dot.x, dot.y);

            if (dis_to_center < 3000) {
                draw_dots(dot);
            }

            if(dot.r > 100){
                dot.r = 100;
            }

            if (dot.y >= (window.innerHeight - (dot.r + 5))){
                if(dotsDropped <= 60000){
                    dotsDropped++;
                    dot.y = window.innerHeight;
                    dotsDropped += 1;
                    dot.vy = 0;
                    dot.vx = 0;
                } else {
                    // dot.y = 0;
                }
                // dot.r += 0.02;
                // dot.r = 100;
                // console.log("Hello Dude");
            }
        }
    }

    ///////End dot script//////

    function start() {
        window.requestAnimFrame(start);
        ctx.clearRect(0, 0, map_w, map_h);
        update_dots();
        // console.log(dotsDropped);
    }

    start();
}());
