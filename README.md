# proiect-openscad
OpenScad
Iga (Voronianu) Sanda Florina
Master PABD anul I 2018

Cu  aplicatia  OpenScad am proiectat:
-  un  copac cu  mai  multe ramuri  si frunze  

module simple_tree(size, dna, n) {   
        if (n > 0)
{
            // trunk
            cylinder(r1=size/10,r2=size/12, h=size, $fn=18);
            //branches
translate([0,0,size])
                for(bd= dna) {
angx = bd[0];                   
angz = bd[1];                   
scal = bd[2];                    
 rotate([angx,0,angz])                           
simple_tree(scal*size, dna, n-1);
                }
        }
        else // leaves           
color("green")          
scale([1,1,3])              
translate([0,0,size/6])                   
rotate([60,0,0])                      
cylinder(r=size/6,h=size/10);
    }
    // dna is a list
of branching data bd of the tree:
    //      bd[0] - inclination of the branch
    //      bd[1] - Z rotation angle of the branch
    //      bd[2] - relative scale of the branch
    dna = [ [12,  80, 0.85], [55,    0, 0.6], 
            [62, 125,
0.6], [57, -125, 0.6] ];
    simple_tree(50,dna, 5);
-  o  racheta
// increase the visual detail
$fn = 100;
// the main
body :
//  a cylinder
ocket_d =50;  // 5 cm wide
rocket_r =rocket_d / 2;
rocket_h =100; // 10 cm tall
cylinder(d =rocket_d, h = rocket_h);
// the head
//  a cone
head_d =40;    // 4 cm wide
head_r =head_d / 2;
head_h =40;    // 4 cm tall
// prepare atriangle
tri_base =head_r;
tri_height =head_h;
tri_points =[ [0,0]
    [tri_base,0],
    [0,tri_height]];
// rotation
around X-axis and then 360° around Z-axis
// put it on
top of rocket's bod

translate([0,0,rocket_h])
    rotate_extrude(angle = 360)
        polygon(tri_points);
// the wings
// 3xtriangles
wing_w = 2;// 2 mm thick
many =3;   // 3x wings
wing_l =40;    // length
wing_h =40;    // height
wing_points
= [[0,0],[wing_l,0],[0,wing_h]];
modulewing() {
    // let it a bit inside the main body
    in_by = 1; // 1 mm
    // set it up on the rocket's perimeter

    translate([rocket_r - in_by,0,0])
        // set it upright by rotating around
X-axis
        rotate([90,0,0])
            // set some width and center it
            linear_extrude(height =
wing_w,center = true)
                // make a triangle

                polygon(wing_points);
}

for (i =[0:many-1]
   rotate([0,0,360/many*i])
   wing();
content ="Iga Sanda Florina";
font ="Liberation Sans";
translate
([-200,270,0])
{
   linear_extrude(height = 5)
   {
       text(content, font = font, size = 15);
     }
 }



