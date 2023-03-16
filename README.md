/* 
    Codebox Rotating Message Script
    -------------------------------
    Usage:
        function go(){
            o = CODEBOX.rotatingMsg.makeTextObject(); 
            o.setParent(parentDiv);
            o.setMessage('Xbox 360'); 
            o.setCentre(400,260);
            o.start();
        }
    Tweak the values in the 'prefs' object to adjust the colour, size, speed and orientation of the message.
    
	For latest version go to: 
		http://codebox.org.uk/pages/javascript/rotating-message
	For licensing information go to: 
		http://codebox.org.uk/pages/about
    
*/
if (CODEBOX===undefined){
    var CODEBOX = {};
}
CODEBOX.rotatingMsg = {};

CODEBOX.rotatingMsg.makeTextObject = function(){
    var obj = {};
    
    /*
        oX, oY          - centre of rotation, in pixels measured from the top-left corner of the screen
        interval        - milliseconds between each update
        spacing         - space between letters, 0 = no space
        inv_delta       - speed, 1 = fastest, 10 = reasonable speed (0 = error)
        size_base       - average size of the letters, in pixels
        size_variance   - amount by which the letters increase/decrease in size, relative to 'size-base'
        x_radius        - number of pixels which the letters move, to the left and right of the centre coordinates
        y_radius        - number of pixels which the letters move, above and below the centre coordinates
        view_from_above - 'true' means the viewer looks down on the circle described by 
                          the letters, 'false' means the viewer looks up
        fade_from_col   - contains the red, green, and blue components of the colour of the letters
                          at the front of the circle, example value: { 'r' : 0, 'g' : 0, 'b' : 0 }
        fade_to_col     - contains the red, green, and blue components of the colour of the letters
                          at the back of the circle, example value: { 'r' : 200, 'g' : 200, 'b' : 200 }
    */
    var prefs = {
        'oX' : 400,
        'oY' : 100,
        'interval' : 40,
        'spacing' : 5,
        'inv_delta' : 10,
        'size_variance' : 20,
        'size_base' : 40,
        'x_radius' : 100,
        'y_radius' : 10,
        'view_from_above' : true,
        'fade_from_col' : {
            'r' : 0,
            'g' : 0,
            'b' : 0
            },
        'fade_to_col' : {
            'r' : 200,
            'g' : 200,
            'b' : 200
        }
    };

    var counter=0;
    var isRunning = false;
    var letters = [];
    var timer;
    var parent = document.body;
    
    function process(){
        counter++;

        for (var i=0; i<letters.length; i++){
            boxData = letters[i];
            updateBoxData(boxData, counter);
            draw(boxData);                    
        }
    }
    
    function updateBoxData(boxData, c){
        c -= boxData.offset;
        boxData.h = Math.floor(prefs.size_base + Math.cos(Math.PI + c/prefs.inv_delta) * prefs.size_variance);
        boxData.w = Math.floor(prefs.size_base + Math.cos(Math.PI + c/prefs.inv_delta) * prefs.size_variance);
        
        boxData.x = Math.floor(Math.sin(c/prefs.inv_delta) * prefs.x_radius);
        boxData.y = Math.floor(Math.cos(c/prefs.inv_delta) * prefs.y_radius);
    }
    
    function draw(boxData){
        var box = boxData.obj;
        
        var topValue    = Math.floor(prefs.oY + (prefs.view_from_above ? -1 : 1 ) * boxData.y - boxData.h/2);
        var leftValue   = Math.floor(prefs.oX + boxData.x - boxData.w/2);
        var colourValue = makeColour(((prefs.y_radius + boxData.y) / prefs.y_radius) / 2);
        
        var newStyle = ['position: absolute; top: ', topValue, 
                'px; left: '      , leftValue,
                'px; height: '    , boxData.h,
                'px; width: '     , boxData.w, 
                'px; font-size: ' , boxData.h,
                'px; color: '     , colourValue
            ].join('');
            
     // Setting everything in 1 go like this reduces re-flows and makes it run a lot faster
        box.style.cssText = newStyle;
    }
    
    function makeColour(n){
     // n will vary from 0 to 1
         function calcColour(n, from, to) {
             var colValue = Math.floor(from - n * (from - to));
             var colHex = colValue.toString(16);
             if (colHex.length===1){
                 colHex = '0' + colHex;    
             }
             return colHex;
         }
         
         var r = calcColour(n, prefs.fade_from_col.r, prefs.fade_to_col.r);
         var g = calcColour(n, prefs.fade_from_col.g, prefs.fade_to_col.g);
         var b = calcColour(n, prefs.fade_from_col.b, prefs.fade_to_col.b);
         
        return '#' + r + g + b;
    }

    obj.setCentre = function(x, y){
        prefs.oX = x;
        prefs.oY = y;
    }
    
    obj.setParent = function(el){
		parent = el;
    }
    
    obj.setMessage = function(msg){
        letters = [];
        
        for (var i=0; i < msg.length; i++){
            add(msg.charAt(i), prefs.spacing * i);    
        }
        
        function add(text, offset){
         // Creates a new 'letter' object and adds it to the letters array
            var letter = {};
            letter.offset = offset;
            
         // Make a absolutely-positioned div to hold the letter
            var box = document.createElement('div');
            box.style.height = '15px';
            box.style.width  = '15px';
            box.style.position = 'absolute';
            
            parent.appendChild(box);
            
            var txt = document.createTextNode(text);
            box.appendChild(txt);
            
         // Make sure the letter object has a reference to its div                        
            letter.obj = box;
                
            letters.push(letter);
        }
        
    }
    
    obj.setInterval = function(i){
        prefs.interval = i;
    }

    obj.start = function(){
        if (!isRunning) {
            if (! letters || letters.length ===0){
                obj.setMessage('Test');
            }
            timer = setInterval(process, prefs.interval)
            isRunning = true;    
        }
    }
    
    obj.stop = function(){
        if (isRunning) {
            clearInterval(timer);
            isRunning = false;
        }
    }
    
    obj.isStarted = function(){
        return isRunning;    
    }
    
    return obj;
}

function go(){
    o = CODEBOX.rotatingMsg.makeTextObject();
    o.setParent(document.getElementById('msgContainer'));
    o.setMessage('Codebox');
    o.setCentre(150,50);
    o.start();
}
window.addEventListener('load', go);
