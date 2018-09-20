+++
date = "2018-08-06"
title = "Building physical objects with code"
tags = ["technical", "CAD"]
math="false"
+++

## 3D printing is really neat!

I recently discovered that my awesome, independently-owned, [local UPS store](http://www.theupsstore.ca/477/) has a pretty sweet 3D printer.

Coincidentally, I was working on a home automation project that really needed a custom part.

The full story of that project deserves it's own substantial blog post. But for now, I want to share with you something amazing I learned.

## What's a CAD?

Computer-Aided Design (CAD) software is used, albeit not exclusively, for designing 3D models. These can be used in games, animation or, in our case, 3D printing.

Going into this, I knew nothing about CAD. I'm a programmer, but I had never dabbled in 3D rendering.

Being a big ol' (GNU?)/Linux geek, I prefer my software to be open-source (or free, as in freedom, or libre, or whatever). I'd heard of [Blender](https://www.blender.org/) as being a very powerful 3D creation software, so I checked it out.

## OK, maybe too powerful

I was immediately overwhelmed. The user interface of most modern 3D CAD software is a mouse-based GUI. While very powerful, they have a steep learning curve. I didn't need 1% of the features of Blender, and I really wanted to design my object now!

## OpenSCAD to the rescue!

It's tagline immediately caught my attention: 

> The Programmers Solid 3D CAD Modeller

Wow! That sounds right up my alley!

With [OpenSCAD](http://www.openscad.org), you use text to describe 3D objects, and then it faithfully renders your object. Perfect for a coder!

You have basic solid geometric shapes to choose from, like cubes and spheres. 

To create a basic rectangular prism, or cuboid as they are apparently called:

```

cube([2,3,4]);

```

You can see what this looks like in this screenshot:

<figure class="blog-figure">
<img src="/images/Openscad_cube.jpg" alt="OpenSCAD screenshot"/>
<figcaption>
Image is from tutorial 
<a href="http://edutechwiki.unige.ch/en/OpenScad_beginners_tutorial" target="_blank">found here
</a>
</figcaption>
</figure>

There are lots of features that are familiar to programmers:

* variables
* functions

Transformations:

* rotate([x,y,z])
* scale([x,y,z])

And the very powerful Boolean operations. They are used to build up more complex shapes:

* union()
* difference()
* intersection()

Check out the cheat sheet to get a better idea of the options:

<figure class="blog-figure">
<img src="/images/openSCAD_cheet_sheet.png" alt="OpenSCAD command cheat sheet"/>
<figcaption>
Image is from official docs
<a href="http://www.openscad.org/documentation.html" target="_blank">found here
</a>
</figcaption>
</figure>

## Complex shapes

More complicated shapes can be made by joining ( `union()` ),  subtracting ( `difference()` ) or subtracting just where they overlap ( `intersection()` ) two shapes.

Here is how we could put a hole in our cuboid from earlier: 

```
difference() { 
  cube([2,3,4], center=true);
  cube([1,2,6], center=true);
}

```

<figure class="blog-figure">
<img src="/images/openscad_diff2.png" alt="OpenSCAD screenshot showing example of the difference operation"/>
<figcaption>
 <code>difference()</code> in action
</figcaption>
</figure>

<figure class="blog-figure">
<img src="/images/openscad_diff.png" alt="Another OpenSCAD screenshot showing example of the difference operation"/>
<figcaption>
Another angle
</figcaption>
</figure>

Note that I centered the shapes ( `center=true` ) because it makes the example simpler.

Also note that the second cube is 1 unit smaller in the X and Y axis, but 1 unit larger in the Z access. This is to ensure the hole goes all the way through and we have a valid result.

## OK, show me what you made!

What I made is basically a shell that goes around a doorknob. It has mounts for a stepper motor which will lock and unlock my doorknob.

For this to work, everything has to be within very tight tolerances. I measured and re-measured, using bits of string. I also eyeballed the mounts for the stepper motor. I'm not even kidding. I closed one eye, and held up the stepper motor in front of my monitor to figure out the placement of the standoffs.

Here it is, in all it's glory:

<figure class="blog-figure">
<img src="/images/openscad_knob.png" alt="OpenSCAD screenshot showing the part I designed"/>
<figcaption>
 Knob-covering stepper motor mount
</figcaption>
</figure>

```

intersection() {
    difference() {
        union() {
            difference() {
                
                // outside tapered cylinder shell
                cylinder(h=48,r1=23,r2=26.5,center=true);
                
                // the hollow center
                cylinder(h=44,r1=22,r2=25.5,center=true);
                
                translate([0,0,-23]) {
                    // rear z-axis hole
                    cylinder(h=2,r=19,center=true);
                    }
                    
                translate([0,0,23]) {
                    // front z-axis hole
                    cylinder(h=2,r=18,center=true);
                    }
            }
            
            // standoffs for mounting stepper motor
            translate([9,19,30]) {
                
                cylinder(h=12,r=3,center=true);
                }
                
            translate([9,-19,30]) {
                cylinder(h=12,r=3,center=true);
                }
        }
        // split whole object in two
        translate([0,1,24]) {
                cube([100,1,100], center = true);
        }
    }
}


```

## But does it fit?

Drumroll please...

Yes, it fits! My very first 3D printed part was close enough as to be almost perfect. All that string and eyeballing must have worked.

## It's not all sunshine and rainbows

That celebration was premature. The super-cheap 5V stepper motor has enough torque to lock the doorknob, but not to reliably unlock it.

The devil, as always, is in the details. I have to take a sabatical from this part of the project, but I have a few ideas up my sleeve to make it work in the future:

* Disassemble and lubricate the doorknob mechanisms to reduce friction

* Run the stepper motor at 9 volts. It claims to be able to handle that

## Stay tuned

If you read this far, congratulations! You deserve a prize. I'm not actually going to give you one, but you deserve one all the same.

I'll have more posts detailing other aspects of this home automation project that I refer to as "doorman", or check out [my github](https://github.com/jeremy21212121) to see some of my other doorman-* repos.
