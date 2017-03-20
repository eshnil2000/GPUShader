# Example Shader run on Shadertoy, no GPU setup required
# out vec4 fragColor is the output from the GPU. in vec2 fragCoord is input to the GPU

# A shader's sole purpose is to return four numbers: r, g, b,and a, returned as a vec4.
 
# Assume Channel0 is a video with green background, and is the default input
# Wherever the green component is dominanant (texColor0.r+texColor0.b) < texColor0.g, use 
# data from Channel1

# If something is not a built in variable, you can send that information from the CPU (your main program) to the GPU (your shader). ShaderToy handles that for us. You can see all the variables being passed to the shader in the Shader Inputs tab. Variables passed in this way from CPU to GPU are called uniform in GLSL. 

# GPUShader
Example for shadertoy

void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    vec2 xy = fragCoord.xy / iResolution.xy;//Condensing this into one line
    vec4 texColor0=texture(iChannel0,xy);
    vec4 texColor1=texture(iChannel1,xy);
    
    if ((texColor0.r+texColor0.b) < texColor0.g){
        fragColor= texColor1;
    }
    else {
        fragColor=texColor0;
    }
}

# Shader Inputs
Shader Inputs
uniform vec3      iResolution;           // viewport resolution (in pixels)
uniform float     iGlobalTime;           // shader playback time (in seconds)
uniform float     iTimeDelta;            // render time (in seconds)
uniform int       iFrame;                // shader playback frame
uniform float     iChannelTime[4];       // channel playback time (in seconds)
uniform vec3      iChannelResolution[4]; // channel resolution (in pixels)
uniform vec4      iMouse;                // mouse pixel coords. xy: current (if MLB down), zw: click
uniform samplerXX iChannel0..3;          // input channel. XX = 2D/Cube
uniform vec4      iDate;                 // (year, month, day, time in seconds)
uniform float     iSampleRate;           // sound sample rate (i.e., 44100)

