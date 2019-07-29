Documentation Author: Niko Procopi 2019

This tutorial was designed for Visual Studio 2017 / 2019
If the solution does not compile, retarget the solution
to a different version of the Windows SDK. If you do not
have any version of the Windows SDK, it can be installed
from the Visual Studio Installer Tool

Welcome to the Specular Map Tutorial!
Prerequesite: Specular Lighting

Comparison Screenshot:
Left:   texture + normal + anisotropy
Middle: texture + normal + anisotropy + specular lighting
Right:  texture + normal + anisotropy + specular mapping

The tutorial for Specular lighting made everything shinny,
but the problem was that everything was equally shinny,
and most surfaces looked more shinny than they should've looked
Specular mapping can apply a different amount of shinniness to each
pixel on the screen

What is a specular map:
A specular map is usually grayscale (black, gray, and white)
For beginners, the Red, Green, and Blue values are all the same
For advanced, you can build an image that only has a Red channel,
without a Green or Blue channel

How it works:
Before adding "finalSpecularColor" to "gl_FragColor" in the GLSL shader,
we multiply the specular color by a pixel color (0 to 1) on a specular map.
Therefore, a darker pixel on a specular map will result in less shinniness,
and a brighter pixel will result in more shininess

How to implement (part 1):
With the exact same programming for color and normal maps, 
you need to load specular map to the material in main.cpp.
You'll need to add a texture:
	char specularTexFS[] = "specularMap";
You'll need to add the file:
	char specularTexFile[] ="../Assets/Specular.png";
You'll need to set the texture to the material:
    material->SetTexture(specularTexFS, new Texture(specularTexFile));

How to implement (part 2):
In fragment.glsl, we need to read this texture, just like the color and normal
You'll need to add a sampler2D:
	uniform sampler2D specularMap;
You'll need to get a pixel from this map:
	vec4 specularColor = texture(specularMap, uv);
In the last tutorial, we calculated specular light with this formula:
	vec4 finalSpecularColor = specularColor * pointLightColor;
All we have to do is change that formula to this:
	vec4 finalSpecularColor = specularColor * pointLightColor * specularLight;
Then, we have variation in shinniness, depending on the pixel of the specular map
We're done! We have specular mapping

How to improve:
(Next tutorial)
	Learn about Skyboxes, Cubemap, and reflections.
	The skybox is reflected off the surface, depending on 
	how bright the specular map pixels are.
