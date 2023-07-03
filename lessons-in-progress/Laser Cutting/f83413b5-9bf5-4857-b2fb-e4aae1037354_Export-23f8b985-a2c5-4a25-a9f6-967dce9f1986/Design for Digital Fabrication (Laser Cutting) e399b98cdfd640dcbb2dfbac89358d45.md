# Design for Digital Fabrication (Laser Cutting)



Categories: Lesson
Created: April 20, 2023 11:58 PM
Review: Currently Working On
Tags: 3D Printing, Advanced Manufacturing

📌 ********************Outlines:******************** A short description of what you can expect in the upcoming section.
📑 **Explanation text:** Written explanations with supporting images.
👩‍🏫 ************************************Explanation videos:************************************ Explaining the course material in short lecture videos.
📺 **Tutorial videos:** Follow-along tutorials.
💡 T********************ips:******************** Tips and tricks to make working in Rhino/Grasshopper easier.
🖱️ **Exercises:** Small practice questions. The solution is provided.
💻 **Assignments:** Open-ended assignments, to practice further with the course materials.

This tutorial will teach you the workflow on how to prepare your Rhino geometry for digital fabrication, specifically laser cutting. The workflow includes techniques such as creating contour slices of the geometry, creating intersecting joints between the slices, orienting the slices onto the cutting plane, optimizing the packing layout with OpenNest plugin, and exporting the curves for laser cutting.

First, we will start with the process of creating contours from a 3D geometry. This step will involve dissecting a 3D model into a series of 2D sections or 'slices' using intersecting planes in Grasshopper. 

Next, we'll move to finding the intersections between slices and cut joints between the slices. This step is important to ensure the slices can be joined and assembled together.

Once we have our finished slices, the third stage will involve orienting these slices flat onto the cutting plane. 

In the fourth step, we will concentrate on how to efficiently pack these slices inside the cutting plate. We'll use the OpenNest plugin, a powerful tool for layout optimization, to help you minimize waste and maximize the usage of your material sheet.

Finally, we will wrap up by showing you how to export these curves for laser cutting. This will prepare you to take your designs from the virtual space of Grasshopper into the real-world process of laser cutting.

By the end of this tutorial, you will have a solid understanding of these essential laser cutting preparation techniques in Rhino Grasshopper. 

# Preparing the Geometry

Welcome to the first section of our laser cutting preparation tutorial. Here, we will introduce the geometry we'll be using for this lesson: a simple bench. This bench will serve as a practical example throughout our tutorial, allowing us to delve deep into the techniques required for preparing a 3D model for laser cutting.

Firstly, let's understand our geometry. A bench, in its most basic form, consists of a seat and legs, potentially with a backrest. In the realm of 3D modeling, we can represent these components with a series of curves and surfaces. It's these elements that we'll be preparing for laser cutting.

To create our bench, we'll be using the sweep function in Rhino Grasshopper. The sweep function allows us to create a surface by 'sweeping' a curve (or multiple curves) along a path, defined by another curve. In the case of our bench, these paths and shapes will be the bench's legs, seat, and if included, the backrest.

To begin, we will first draw the curves that define the profiles of these elements. This includes creating two-dimensional profiles for each leg, the seat, and the backrest, if necessary. These profiles should be drawn to scale, reflecting the actual dimensions you want for your bench.

Once we've drawn these curves, we will then apply the sweep function. This function takes two main inputs: the curve(s) to be swept and the path along which they should be swept. In our case, the curves we've drawn will be the elements to be swept, and the paths will be the lines defining the length, width, and height of the bench.

By using the sweep function, we'll transform our two-dimensional curves into a three-dimensional bench model. This model will then serve as the starting point for our contour slicing and plate packing processes in the later sections of this tutorial.

By the end of this section, you'll have a solid understanding of how to create a 3D model using curves and the sweep function. You'll also have your own bench model, ready for the next steps in the laser cutting preparation process.

In the next section, we'll move onto dissecting our bench model using contour slicing. But for now, let's get sweeping and create our bench!

![Screenshot 2023-06-28 at 23.37.41.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.37.41.png)

![Screenshot 2023-06-28 at 17.37.47.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_17.37.47.png)

![Screenshot 2023-06-28 at 17.38.40.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_17.38.40.png)

![Screenshot 2023-06-28 at 17.39.36.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_17.39.36.png)

![Untitled](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Untitled.png)

# Paneling/Contouring the Surface

Now that we've created our 3D bench model, it's time to start preparing it for laser cutting. In this section, we'll slice our model into both vertical and horizontal sections using intersecting planes.

In Grasshopper, the 'Plane' component allows us to define a 2D plane in 3D space. We'll use these planes as 'cutting boards' to slice through our 3D bench model. We'll create two sets of planes: one set that's horizontal (parallel to the ground plane) and one set that's vertical (perpendicular to the ground plane).

For the horizontal slices, we'll first define the interval at which we want our slices. The intervals you choose will depend on the thickness of the material you plan to use for laser cutting. For instance, if you're using 5mm plywood, you may want your slices to be spaced 5mm apart to represent each layer of plywood.

To generate these horizontal planes, we'll use the 'Series' component in Grasshopper. We'll plug our chosen interval into this component, along with the total height of the bench, to create a series of numbers that represent the heights at which we want our planes to intersect the bench.

Next, we'll feed these numbers into a 'Rectangle' component to generate a series of horizontal planes at these heights. Then, we'll use the 'Brep | Plane' component (also known as the 'Intersection' component) to create the intersection curves between these planes and our bench model.

The process is similar for the vertical slices. The main difference is that we'll be creating vertical rectangles for the planes instead of horizontal ones. The intersection between these planes and our bench model will give us the vertical slices of our model.

By the end of this section, you'll have a series of curves that represent the horizontal and vertical slices of your bench model. These curves will be our starting point for the next section, where we'll orient these slices onto our cutting plane.

Remember, the precision with which we do this step will directly impact the accuracy of our final laser cut model. So, take your time, check your work, and let's move onto creating those slices!

![Screenshot 2023-06-28 at 23.36.11.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.36.11.png)

![Screenshot 2023-06-28 at 17.49.37.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_17.49.37.png)

![Screenshot 2023-06-28 at 22.44.24.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_22.44.24.png)

![Screenshot 2023-06-28 at 22.44.52.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_22.44.52.png)

![Screenshot 2023-06-28 at 23.34.05.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.34.05.png)

![Screenshot 2023-06-28 at 22.42.33.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_22.42.33.png)

![Screenshot 2023-06-28 at 22.46.18.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_22.46.18.png)

![Screenshot 2023-06-28 at 23.28.11.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.28.11.png)

![Untitled](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Untitled%201.png)

# Find Intersections and Cut the Panels

Welcome to the third part of our tutorial where we'll address one of the most critical aspects of preparing your model for laser cutting - finding intersections and cutting the joints between slices.

Now that we have both our horizontal and vertical slices, it's time to determine where they intersect. This information will allow us to create notches at the intersections, facilitating the assembly of our laser-cut pieces into a 3D form.

In Rhino Grasshopper, the 'Curve | Curve' component helps us find the intersections between two curves. In our case, we'll be using this component to find the intersection points between our vertical and horizontal slices. We input our series of horizontal and vertical slice curves into the component, and it will output the points where these slices intersect.

These intersection points will serve as the center of our notches. To cut these notches, we need to create a notch geometry that matches the thickness of our material. For instance, if we're using 5mm plywood, our notches should be 5mm wide to allow the pieces to slot together snugly.

We will create this notch geometry using the 'Rectangle' component in Grasshopper. We'll input the width (matching the thickness of our material) and the height (you can experiment with this value, but a good starting point might be half the height of your slices). This will generate a series of rectangles that represent our notches.

Next, we'll position these notches on our slices using the 'Move' component in Grasshopper. We'll input the notches and the intersection points into the 'Move' component, which will place the notches at the intersection points.

Finally, we'll cut these notches out of our slices using the 'Region Difference' component. We'll input our slices and notches into this component, which will subtract the notch geometry from the slices, leaving us with slices that have notches cut out at the intersections.

By the end of this section, your slices will be ready for laser cutting, with notches cut out at the intersections. In the next part, we will proceed to orient these slices onto our cutting plane. This will put us one step closer to our final goal of laser cutting and assembling our 3D bench model.

![Screenshot 2023-06-28 at 23.26.01.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.26.01.png)

![Screenshot 2023-06-28 at 23.09.41.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.09.41.png)

![Screenshot 2023-06-28 at 23.10.43.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.10.43.png)

![Screenshot 2023-06-28 at 23.29.03.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.29.03.png)

![Screenshot 2023-06-28 at 23.11.38.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.11.38.png)

![Untitled](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Untitled%202.png)

# Orient the Panels Flat

In this section, we'll introduce the use of a powerful Grasshopper plugin, OpenNest, to orient our slices flat onto the cutting plane. OpenNest is a freely available open-source plugin designed to optimize part arrangement and nesting, making it an invaluable tool for digital fabrication processes. You can download the plugin from this link: **[OpenNest Plugin](https://www.food4rhino.com/en/app/opennest)**.

OpenNest excels in situations like ours, where numerous uniquely shaped slices need to be fit onto a flat sheet of material. It employs intelligent algorithms to place these parts to maximize material usage and minimize waste, while also ensuring that all parts stay within the boundaries of the sheet material.

After you've downloaded and installed the OpenNest plugin in Grasshopper, we'll start setting up our primary inputs using the 'Pack Objects' component:

1. **Geometries:** This input takes the slices we've prepared as its data. Ensure these curves are flattened before connecting them to the 'Geometries' parameter of the 'Pack Objects' component.
2. **Sheet Size:** For the 'Sheet Size' parameter, provide the dimensions of your cutting material to define the boundaries of your cutting plane.

Once you've set these inputs, OpenNest automatically processes the data, returning an optimized configuration that arranges our slices onto the cutting plane, viewable in the Rhino viewport.

By the end of this section, your slices will be well-arranged onto the cutting plane, ready for cutting. OpenNest truly showcases its strength here by saving significant time and effort that would otherwise be used in manually arranging each part, especially when dealing with complex geometries and a large number of slices.

As we approach the final section of this tutorial, we'll show you how to export these arranged slices to ready them for the laser cutting process.

![Screenshot 2023-06-28 at 23.24.27.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.24.27.png)

![Untitled](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Untitled%203.png)

# Optimally Pack the Panels into the Cutting Piece

Now we will leverage the power of the OpenNest plugin to pack our slices optimally onto the cutting plane. This is an important step in the preparation process, aimed at maximizing material usage and minimizing waste.

Once you have your slices oriented flat on the cutting plane with the 'Pack Objects' component, it's time to initiate the nesting process using the main 'OpenNest' component.

The 'OpenNest' component takes several inputs, but we will primarily focus on three of them:

1. **Geometries:** This will be the slices from our previous step.
2. **Sheet definition:** This will be the size of the cutting material, same as what we used with the 'Pack Objects' component.
3. **Iterations:** This input determines how many iterations the algorithm will perform to try and find the most efficient arrangement. The higher the number, the longer the computation, but potentially the better the result.

Upon setting these inputs, OpenNest will process the data and generate an optimized configuration that packs our slices onto the cutting plane as efficiently as possible. The result can be previewed in the Rhino viewport.

It's important to note that each run may yield a slightly different result due to the algorithm's nature. If you are not satisfied with the initial result, feel free to adjust the number of iterations or rerun the process until you achieve a desirable output.

By the end of this section, you'll have a nested configuration of your slices on the cutting plane. The optimization provided by OpenNest should ensure that you are maximizing the use of your material and reducing waste.

Next, in the final part of our tutorial, we will export these nested slices, preparing them for the laser cutting process. So, let's dive into the nesting world with OpenNest!

![Screenshot 2023-06-28 at 23.23.40.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.23.40.png)

![Untitled](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Untitled%204.png)

# Generate the Cutting File

Having optimally packed our slices onto the cutting plane using OpenNest, the next step is to bake these curves in Rhino and export them as a DXF file. DXF (Drawing Exchange Format) is a widely accepted format for CNC operations, including laser cutting.

To begin, we'll 'bake' our curves from Grasshopper into Rhino. In Grasshopper, 'baking' refers to the process of transforming algorithmically generated geometry into actual geometry in the Rhino workspace. To do this, simply right-click on the 'Geometries' output from the 'OpenNest' component and select 'Bake'. This will transfer the nested slices into Rhino.

Once your geometries are baked into the Rhino environment, select the curves and proceed to exporting as a DXF. To do this, go to 'File' > 'Export Selected'. In the dialog box that appears, choose 'DXF' from the 'Save as type' dropdown list.

Before finalizing the export, a 'DXF Export Options' window will appear. Here, you'll need to select the appropriate settings for your laser cutter. The options vary, but you usually need to specify the DXF version (usually the latest, or as specified by your laser cutter's requirements), the units (typically the same as your Rhino document's units), and whether you want to export as curves, polylines, or other entities.

By the end of this section, you should have a DXF file with your optimally packed slices, ready for the laser cutting process. Please review the file before cutting, making sure that the geometry looks correct and is within the bounds of your material size.

Congratulations! You've successfully navigated the process of preparing a geometry for laser cutting using Rhino, Grasshopper, and the OpenNest plugin. We wish you the best of luck in your fabrication endeavors and can't wait to see the fantastic 3D structures you create from these 2D slices!

![Screenshot 2023-06-28 at 23.21.43.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.21.43.png)

![Screenshot 2023-06-28 at 23.16.28.png](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Screenshot_2023-06-28_at_23.16.28.png)

![Untitled](Design%20for%20Digital%20Fabrication%20(Laser%20Cutting)%20e399b98cdfd640dcbb2dfbac89358d45/Untitled%205.png)