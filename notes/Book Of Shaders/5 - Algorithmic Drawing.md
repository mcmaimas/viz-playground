PreReqs
gl_FragCoord: contains the window-relative coordinates of the current fragment
- (0.5,0.5) is returned for the lower-left-most pixel in a window
- move the (x,y) value to (0,0) with pixel_center_integer

smoothstep: perform Hermite interpolation between two values
- 3 parameters: edge0 (lower edge of hermite function), edge1(upper edge of hermite function), x (source value for interpolation)
- edge0 < x < edge1 (results are undefined if edge0 >= edge1)
- Hermite interpolation: Don't need to know the workings, just that it's a good interpoaltion function

-------------------------------------
Here is my fence:
#ifdef GL_ES
precision mediump float;
#endif

uniform vec2 u_resolution; // The resolution of the screen aka, pixels wide by pixels high
uniform vec2 u_mouse; // Position of the mouse
uniform float u_time; // Some amount of time has passed

// Plot a line on Y using a value between 0.0-1.0
float plot(vec2 st) {
    // edge0 is 0.02
    // edge1 is 0.0
    // x is absolute value of st.y - st.x 
    return smoothstep(0.02, 0.0, abs(st.y - st.x));
}

void main() {
  // Get the normalized coordinates of the pixel (normalized just means the values are scaled so they fit between 0 and 1)
	vec2 st = gl_FragCoord.xy/u_resolution;
    
    // Save the current value of x into a new variable y. Idk why we do this, maybe we don't want to pass st.x around freely
    float y = st.x;

    // vec3 rgb: Give me a uniform grey color please r=y, g=y, b=y
    // probably obvious but I had never thought of it. black is 0,0,0 white is 1,1,1 and all of the pure greys are when r=g=b
    vec3 color = vec3(y);

    // Plot a line
    // What exactly is the return value of plot????? It's the pct but i'm not 100% clear on the percent of what
    // If it's the pct 
    // t = clamp((x - a) / (b - a), 0, 1)
    // return t * t * (3 - 2 * t)
    // and clamp is min(max(x, minVal), maxVal)
    float pct = plot(st);

    //When perecnt is 1.0, show full on green. When pct is 0.0, show black/white gradient
    //That means that plot returns 1 only when x=y, aka why the line is green
    color = (1.0-pct)*color+pct*vec3(0.0,1.0,0.0);

  // vec4 is rgba
	gl_FragColor = vec4(color,1.0);

step: first value is the limit or threshold and second value is the value we want to check. returns 0.0 or 1.0
smoothstep: Given a range of 2 numbers and value. this function will interpolate the value between the defined range
- still a lot of questions here, but move on for now

what drives me wild is smoothstep. The page says if edge0 is ever greater than or equal to edge1 then results will be undefined. Since 0.02 (edge0) and 0.0(edge1) are hardcoded as the first 2 params then how is this function not always undefined

sine and cosine: They automatically return values between -1 and 1 and that makes them incredible to have in the toolkit