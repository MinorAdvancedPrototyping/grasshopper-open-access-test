# Design for Personalized Fit

Categories: Lesson
Created: April 28, 2023 4:05 PM
Review: Ready for Review
Tags: 3d scans, personalized

📌 ********************Outlines:******************** A short description of what you can expect in the upcoming section.
📑 **Explanation text:** Written explanations with supporting images.
👩‍🏫 ************************************Explanation videos:************************************ Explaining the course material in short lecture videos.
📺 **Tutorial videos:** Follow-along tutorials.
💡 T********************ips:******************** Tips and tricks to make working in Rhino/Grasshopper easier.
🖱️ **Exercises:** Small practice questions. The solution is provided.
💻 **Assignments:** Open-ended assignments, to practice further with the course materials.

Special thanks to Dr. Wolf Song and Dr. Toon Huysmans for developing part of the content in this lesson.

- Exercise Files:
    
    [Personalized Design From 3D Scan - Hand Splint Exercise.gh](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Personalized_Design_From_3D_Scan_-_Hand_Splint_Exercise.gh)
    
    [Generating a Mesh from Ear Canal Cavity (Kangaroo Physics)](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/2023_A2_example.gh)
    

# Introduction

<aside>
📑 *What:*         Introduction to the field of personalized design and 3D scanning
*For Whom:* Intermediates in Rhino/Grasshopper
*Time:*          15 minutes

</aside>

## Personalized Design

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled.png)

Personalized design is an innovative approach to creating unique and customized products that are tailored to meet individual needs ranging from functional requirements to aesthetics. There are three main types of personalized products:

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%201.png)

**Personalization in Identity:** focuses on enhancing the perception of the product by giving the customer freedom of customization through unique form, texture, colour, print, smell, taste, sound, feel, etc.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%202.png)

**Personalization in Capabilities:** focuses on enhancing the functions of the product to increase performance through extra augmentations (electrical, mechanical, fluidic, and thermal components) to create added value to the product.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%203.png)

**Personalization in Fit:** focuses on the interaction between the product, consumer, and its environment. Characteristics of the product such as shape, size, mass, colour palette, and personalized interactions (e.g. comfort) are adjusted to meet the individual’s needs.

## Personalization in Fit

The following lesson will focus on Personalization in Fit. This design method relies on physical measurements of an object or body part to generate a custom fitted product to meet the users need. The Personalization in Fit can benefit the users by providing increased comfort and improved performance.

When developing a design for Personalized Fit in Rhino Grasshopper, the goal is to create a Rhino Surface that matches the geometry and dimensions of the body part/object. For more on information on Rhino Surfaces, please refer to Lesson 4 (Reference here). Once the Rhino Surface has been created, the surface can be modified depending on the needs of the user e.g. applying a data-driven algorithmic pattern on the surface to reduce pressure applied on the body. There are various approaches to developing a personalized fit using Rhino Grasshopper depending on the body part and the data input method used.

# Collecting Anthropomorphic Data

<aside>
📑 *What:*         Introduction to the field of personalized design and 3D scanning
*For Whom:* Intermediates in Rhino/Grasshopper
*Time:          20* minutes

</aside>

## Overview of Collection Methods

To begin designing a product personalized for fit, we first need to collect anthropomorphic data (data of the human body geometry) before we create the Grasshopper script to generate the Rhino geometry. Depending on the requirements of the design, there are various collection methods varying in accuracy and complexity. The decision on the collection method will also influence how the Grasshopper script will be set up as we will see in the following section.

The input methods we will discuss include:

- Physical measurements and Contact Based 3D Scanning
- Non-Contact 3D Scanning
- Statistical Shape Modeling
- 3D scan database (DINED)

## Physical Measurements and Contact Based 3D Scanning

Obtaining physical measurements is the simplest and quickest method to acquire data on human body parts, yet it might not be as accurate as other methods. To obtain physical measurements, the designer can use simple tools such as a caliper, or a custom rig to measure specific points along the body. You might already be familiar with some measurement rigs such as the foot measuring device to find your shoe size.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%204.png)

In the Master's graduation project [**Development of a low-cost 3D foot scanner**](Grasshopper_Rhino_course/Graduation_Projects/Development%20of%20a%20low-cost%203D%20foot%20scanner.md) , graduation student [Hoeksema, J.](https://repository.tudelft.nl/islandora/search/author%3A%22Hoeksema%2C%20J.%22) developed a rig to digitally measure specific points along a person's foot as seen in the figure below.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%205.png)

## Non-Contact 3D Scanning

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%206.png)

Non-contact 3D scanning is the process of collecting data on a real world object through cameras, lasers, and other types of sensors. The outcome of this process is usually a 3D mesh model as seen in the figure below.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%207.png)

Depending on the accuracy of the 3D scanned used, the 3D mesh may require some post-processing to reduce the noise, artefacts, and missing data in the scanning process before it is ready for use inside of Grasshopper. The post-processing cleaning of the mesh can be done in a polygon modeling software such as Blender or Zbrush. In some cases, mesh correspondence can also be an option to improve the quality of the 3D scan. In mesh correspondence, a high quality 3D template is overlayed and deformed to match the geometry of the 3D scan as can be seen in the figure below. Mesh correspondence can be done using the software [R3DS Wrap 3](https://www.russian3dscanner.com/download_and_buy/) .

![Credits: Dr. Toon Huysmans](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%208.png)

Credits: Dr. Toon Huysmans

## Statistical Shape Modeling

Statistical Shape Modeling are used to describe a collection of similar 3D data in a simplified way. SSMs represent an average of the geometry of the 3D data including any variation. For example, if you have collected various 3D scanned data of ear geometry from a certain population, using SSM you could create an average 3D mesh model of your collected data. This approach can be useful when the goal of your design is for Personalized Fit of an individual, but Personalized Fit for a particular population. To explore the creation of SSM, refer to the software [Paraview](https://www.paraview.org/) for more information.

![Credits: Dr. Toon Huysmans](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Screenshot_2023-04-20_at_22.51.09.png)

Credits: Dr. Toon Huysmans

## 3D Scan Database (DINED)

If your design project requires Personalization in Fit for a specific human population, online databases such as [DINED](https://dined.io.tudelft.nl/en) are useful to quickly collect data and obtain quality 3D meshes for the human body. DINED is an anthropomorphic database with various data, including 3D data, of various human populations. With DINED, you are able to select from a variety of populations and measures, and download the 3D SSM mesh file as an STL to be used in Grasshopper.

![Credits: Dr. Toon Huysmans](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%209.png)

Credits: Dr. Toon Huysmans

Additionally, there is a Grasshopper plugin for DINED developed at TU Delft - Industrial Design Engineering by Dr. Toon Huysmans. This plugin allows the user to directly select the population and import the 3D STL model directly from Grasshopper. More information on the DINED Grasshopper plugin can be found in the following resource: [DINED Plugin](Grasshopper_Rhino_course/Graduation_Projects/DINED%20Plugin.md) 

# Generating Personalized Designs from Anthropomorphic Data

Depending on your data collection method and the requirements of your design, there are various methods you can take to generate a Rhino Surface using Grasshopper. The first few methods presented showcase how to generate a Rhino Surface using different input data and approaches. A Rhino Surface is often the starting point in your personalized design before adding further features. The final method showcases how a pre-existing design template can be customized using anthropomorphic data collected from users.

## Generating a Surface from Physical Measurements

In this scenario, the designer generates a surface from physical measurements taken of users anthropomorphic data whether it is measured with simple tools like a caliper or a custom rig. For this, the designer creates a Grasshopper script with a template surface. The template surface is created from curves, from which the control points represent the locations at which the measurements are taken.

An example of this scenario can be seen in [**Development of a low-cost 3D foot scanner**](Grasshopper_Rhino_course/Graduation_Projects/Development%20of%20a%20low-cost%203D%20foot%20scanner.md) . In this graduation project, the student developed a custom contact 3D scanning rig to measure the feet of users. The measured location points are then inputted into a Grasshopper script that modifies the surface template to match the measured values.

Let's consider how we can set up a Grasshopper script using a similar scenario to generate a surface of foot based on foot measurements. in our case, we do not have access to a custom measuring rig, but we will rely on simple tools such as a caliper or ruler. We can take the following steps to create our script:

- Decide on the key measurement locations
- Create the surface template using curves with defined control points
    - Can be done in Rhino or Grasshopper
    - Use a 3D scan as a guide if needed
- Define how the physical measurements will affect the location of the points
    - Adjust the distance between points based on the physical measurements

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2010.png)

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2011.png)

## Generating a Surface from 3D Scan (Mesh Slicing)

[Personalized Design From 3D Scan - Hand Splint Exercise.gh](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Personalized_Design_From_3D_Scan_-_Hand_Splint_Exercise.gh)

In this scenario, the goal is to create a surface from a 3D scan of a body part with relatively simple geometry e.g. an arm or leg. Imagine that you would like to create a design for an arm brace using the 3D scan mesh of your user's arm. We can approach this problem in Grasshopper with the following steps;

1. Create a series of planes across the arm

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2012.png)

1. Find the intersection curve between the plane and the mesh

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2013.png)

1. Create a loft between the curves to generate a surface

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2014.png)

For further instructions on how to set up the Grasshopper script, refer to [Lesson 4 - Surfaces](Grasshopper_Rhino_course/Lessons/4️⃣%20Lesson_4-Surfaces/!index.md) 

Additionally, it is important to mention that this method is not only intended for 3d scan anthropomorphic data. In fact, we can apply this method to any 3D scan mesh data we collect. One common use case as a designer is to develop rapid physical prototypes out of a mouldable materials such as clay using the body part of the user as a guide. We can then 3D scan the prototype and generate the surface in Rhino Grasshopper with this approach. The figure below showcases how this method can be applied to create an ergonomic mouse going from a clay prototype to 3D scan mesh to Rhino surface.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2015.png)

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2016.png)

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2017.png)

## Generating a Mesh from a Cavity using a 3D Scan (Physics Simulation)

[Generating a Mesh from Ear Canal Cavity (Kangaroo Physics)](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/2023_A2_example.gh)

For more complicated 3D scan geometry, the approached mentioned above might not be sufficient to generate good results. In this cases, a more creative approach is necessary. Let's take for example, the geometry of an ear canal. in this scenario, we would like to create an earbud that is personalized for the user's 3D scan and perfectly fits the cavity of the ear canal.

One approach we can take is to use Grasshoppers Kangaroo physics simulation to generate the geometry of the earbud. It is important to note that the following approach is for advanced users, only works on Windows PC for now, and requires the following plugins:

- Weaverbird
- Lunchbox
- Pufferfish
- Dendro

If you are new to Grasshopper Kangaroo physics simulation, it is recommended to first read the lesson on (Insert link to Form Finding with Kangaroo Physics). This approach is as follows:

1. Simplify the geometry of the ear to speed up the simulation

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2018.png)

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2019.png)

1. Prepare a distribution of small spheres to collide with the ear canal and set up the simulation with Kangaroo

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2020.png)

1. Run the simulation allowing the spheres to collide with the ear and fill up the ear canal cavity

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2021.png)

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2022.png)

1. Create a volume from the collection of spheres and convert into mesh

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2023.png)

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2024.png)

For more details on this implementation, refer to the example file provided: [Generating a Mesh from Ear Canal Cavity (Kangaroo Physics)](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/!index.md). In this approach, we can adjust the size and shape of the final mesh by adjusting the simulation parameters. For example, if we want the earbud to cover a larger area of the ear, then we can add more balls to the simulation to increase the total area covered by the balls. Experiment with the example file and test it out for yourself!

## Deforming Parametric Model to 3D Scan

In this scenario, the designer creates product in Rhino or in Grasshopper to meet the desired function and form. This design serves as a template that can be customized to meet the size requirements of different users. In the template, certain product parameters are parametrize to adjust based on the size requirements. Using Rhino Grasshopper, a script can be written to automatically extract data from a 3D scan that can be used to adjust the product parameters automatically.

A great example of this method is the [**Design of customizable sunglasses based on additive manufacturing techniques**](Grasshopper_Rhino_course/Graduation_Projects/__Design_of_customizable_sunglasses_based_on_additive_manufacturing_techniques__.md) . In this project, the student created a main design template of sunglasses with some features of the sunglasses being parametrized e.g. parametric temple (side piece) length and bridge (nose piece) length to accommodate various head and nose sizes. By collecting and analyzing data from user's 3D scans, the parametric glasses are automatically adjusted to fit the user's size requirements. A visual example of these results can be seen in the figure below.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2025.png)

To implement this approach in a Grasshopper script, let's consider the above mentioned example. Here we will create a script that adjust the length of the temple of the glasses based on the mean head circumference of the 3D scan with the following steps:

### Simple Method

- Slicing the 3D mesh to create contour curves (z-direction)
- Measuring the average circumference of the contour curves
- Adjusting the Temple Length parameter based on the average circumference

### Advanced Method

- Creating landmark location of the ear and nose bridge (manual or automatic)
- Measuring distance between the two landmark points
- Adjusting the Temple Length of glasses based on this length

- Consulted with Anne, we will do the following
    - Discuss how some advanced 3d scanner software can create landmarks of features (ears, nose)
    - If we do not have access to that software, then we have a manual step to select a point on the ear and on the nose as the starting point
    - Base on this distance, the size of the glasses will adjust accordingly

## Modifying the Personalized Product

Once we have a basic Rhino geometry to work with, we can start modifying the geometry to add value to our user. We can add value to the user in two ways: aesthetics and functionality.

In aesthetics, we can add value by detailing to the surface to make the product more appealing. One simple way to achieve this is to add patterns to surfaces to add unique aesthetic. More detailing on Morphing a Pattern to a Surface can be found in the Mini-Lesson [Morphing a Pattern to a Surface](Grasshopper_Rhino_course/Graduation_Projects/Morphing_a_Pattern_to_a_Surface/!index.md).

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2026.png)

In functionality, we can add value by making the product more comfortable to wear or to support certain areas of the bodies. For this, we will need to collect more data on the user's use case, such as how heat is distributed throughout the body or how the pressure is distributed on the body when wearing the product. This is further discussed in the next lesson [Ergonomic Data Driven Personalized Design](Grasshopper_Rhino_course/Graduation_Projects/Ergonomic_Data_Driven_Personalized_Design/!index.md).

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2027.png)

# Relevant Projects

[Untitled Database](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%20Database.csv)

---

# Draft 1 (archive)

# Preliminary Outline (To be removed)

1. Introduction into personalized design
2. Link to examples from graduation projects
3. Introduction into the example
    1. Generating a forearm splint with custom pattern from a 3d scan
4. Creating the surface
    1. Import 3d scan mesh into Rhino
        1. First open Grasshopper and then import the 3d scan mesh into that instance of Rhino
    2. Create boundary box
    3. Select the direction to divide up the model
    4. Create multiple planes along the model direction
    5. Find intersection curve between 3d scan mesh and the planes
    6. Rebuild the curves
    7. Loft a surface over the curves
5. Creating the pattern
    1. Create a pattern
        1. Pattern can be designed around certain data (heat map, pressure map) but that is covered in another section - link to section
6. Morphing Pattern on Surface
    1. Set up the UV mapping
    2. Morph the pattern onto the surface
7. Optimizing and preparation for 3d printing
    1. Covered in another section - link to section 

# 📑 A.1 Introduction

<aside>
📌 *What:*         Introduction to the field of personalized design and 3D scanning
*For Whom:* Intermediates in Rhino/Grasshopper
*Time:*          15 minutes

</aside>

## Personalized Design

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2028.png)

Personalized design is an innovative approach to creating unique and customized products that are tailored to meet individual needs ranging from functional requirements to aesthetics. There are three main types of personalized products:

1. **Personalization in Identity:** focuses on enhancing the perception of the product by giving the customer freedom of customization through unique form, texture, colour, print, smell, taste, sound, feel, etc. 

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2029.png)

1. **Personalization in Capabilities:** focuses on enhancing the functions of the product to increase performance through extra augmentations (electrical, mechanical, fluidic, and thermal components) to create added value to the product.

![[https://www.pinterest.cl/pin/491103534351777759/](https://www.pinterest.cl/pin/491103534351777759/)](Design%20for%20Personalized%20Fit%201c2469e866924f6eb4adb908398e9992/Untitled%2030.png)

[https://www.pinterest.cl/pin/491103534351777759/](https://www.pinterest.cl/pin/491103534351777759/)

1. **Personalization in Fit:** focuses on the interaction between the product, consumer, and its environment. Characteristics of the product such as shape, size, mass, colour palette, and personalized interactions (e.g. comfort) are adjusted to meet the individual’s needs.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2031.png)

## Personalization in Fit

The following lesson will focus on *******************Personalization in Fit.******************* This design method relies on 3D scanning technology to capture precise measurements of the object or body part to be designed for and then uses algorithms to create custom patterns and shapes. The benefits of **********************Personalization in Fit********************** are numerous, including increased comfort, improved performance, and reduced waste. In this section, we will introduce you to the exciting world of personalized design and show you how to design your own personalized product using 3D scanning data with Rhino and Grasshopper.

# 📑 A.2 Exercise - Designing a Personalized Hand Splint with Custom Pattern

<aside>
📌 *What:*         Introduction to the exercise and design approach
*For Whom:* Intermediates in Rhino/Grasshopper
*Time:*          15 minutes

</aside>

In this section, you will learn how to design a personalized hand splint using 3D scanning data of an arm with Rhino and Grasshopper. The exercise files can be found at the beginning of this lesson to help you follow along during the lesson.

![Source: [https://nl.pinterest.com/pin/377106168771535985/](https://nl.pinterest.com/pin/377106168771535985/)](Design%20for%20Personalized%20Fit%201c2469e866924f6eb4adb908398e9992/Untitled%2032.png)

Source: [https://nl.pinterest.com/pin/377106168771535985/](https://nl.pinterest.com/pin/377106168771535985/)

First, we begin by dissecting the problem/system into manageable parts in a step called **************Decomposition.************** The divided parts are functional elements that collectively comprise the whole system/problem. In this exercise, we will focus on the ******Splint****** component.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2033.png)

The design method involves using algorithms to create a Rhino surface from the 3D scanned mesh, creating custom patterns and shapes to be applied to the splint, and morphing the custom pattern onto the Rhino surface. Let's get started!

## Design Workflow

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2034.png)

- Show overview of the algorithmic process - can be applied to other geometry as well
    - Here include illustration showing the process with the 3d files as well

# 📑A.3 Creating a Surface from a 3D Scan Mesh

The first step in the design method is to create a surface from the imported 3D scan mesh. To learn more on this procedure, refer to [Lesson 4 - Surfaces](Grasshopper_Rhino_course/Lessons/4️⃣%20Lesson_4-Surfaces/!index.md).

# 📑A.4 Generating Custom Pattern

<aside>
📌 *What:*         Design approach for generating a custom pattern
*For Whom:* Intermediates in Rhino/Grasshopper
*Time:          30* minutes

</aside>

In this section, we will show you how to create a custom pattern to apply on the surface of the splint. Custom patterns can be generated for aesthetics or functional needs. Custom patterns for aesthetic needs provide visually interesting designs for the customer. On the other hand, custom patterns for functional needs can be used to increase comfort in the personalized design by adjusting the pattern-based physiological measured data such as heat distribution or pressure on the body. Designing custom patterns for functional needs is covered in [Insert Lesson on Data-driven design]. In this lesson, we will show you how to design a custom pattern for aesthetic needs.

## Approach for Generating Custom Pattern

In the figure below, the general approach for generating a custom pattern for aesthetics is shown. Here, we will utilize a commonly used pattern in computation design called “voronoi”.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2035.png)

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2036.png)

## Voronoi Pattern

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2037.png)

A Voronoi pattern is a type of pattern that is created by dividing a space into cells based on the proximity of points. In the context of design, Voronoi patterns are often used to create organic and intricate designs that are visually interesting. In the process of creating a Voronoi pattern for a personalized design project, the surface is divided into a network of cells based on the proximity of points on the surface. The shape and size of the cells can be adjusted to create different effects based on the needs of the personalized design.

## Defining the Boundary Curve

The first step is to generate the boundary curve where the custom pattern will be created. In this example, a rectangle is created to match the general dimensions of the arm scan. It is important to note that the pattern will deform when it is morph to the 3D surface, therefore, the general proportions of the initial boundary curve should match with the proportions of the morphing surface to avoid unwanted results.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2038.png)

## Populating Random Points

Before generating the voronoi pattern, a distribution of points on the surface is needed to create the network of cells. As we do not want the points to be located on the edge of the boundary curve, we first offset the boundary curve inward using the “Offset Curve” component. The offset curve can then be used as the “Region” input in the “Populate 2D” component. Here you can choose the number of points to be generated with the “Count” input, which will created more cells in the voronoi pattern with a higher number of points. 

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2039.png)

## Creating the Voronoi Pattern

The generated points are then connected as the points in the “Voronoi” components. Based on the proximity of the generated points, the voronoi pattern generates a cell at each of the points’ location. To ensure the pattern extends the all the way to edge of the boundary curve, we connect the original boundary curve, not the offset curve, as the boundary of the voronoi pattern.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2040.png)

## Offsetting the Pattern Curve

To give the voronoi pattern width to be able to generate a surface in the next step, we use the “Offset Curve” component once more. In this step, we must be careful of the constraints in the “Distance” input. Here we choose a low negative value to avoid intersecting curves. Feel free to experiment with setting different “Distance” values and see what the available range is.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2041.png)

## Generating Boundary Surface and Extruding

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2042.png)

# 📑A.5 Applying Pattern on Surface

## Morphing Approach

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2043.png)

### Setting up UV Mapping

# 📑A.6 Beyond This Lesson

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2044.png)

# 📑A.7 Further Reading

Data driven - another lesson

Preparing for 3D Printing - another lesson

# 📑A.8 Example Projects

Here include links to other projects that are already including 

# Draft 2 (archive)

# Introduction

<aside>
📑 *What:*         Introduction to the field of personalized design and 3D scanning
*For Whom:* Intermediates in Rhino/Grasshopper
*Time:*          15 minutes

</aside>

## Personalized Design

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2028.png)

Personalized design is an innovative approach to creating unique and customized products that are tailored to meet individual needs ranging from functional requirements to aesthetics. There are three main types of personalized products:

1. **Personalization in Identity:** focuses on enhancing the perception of the product by giving the customer freedom of customization through unique form, texture, colour, print, smell, taste, sound, feel, etc. 

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2029.png)

1. **Personalization in Capabilities:** focuses on enhancing the functions of the product to increase performance through extra augmentations (electrical, mechanical, fluidic, and thermal components) to create added value to the product.

![[https://www.pinterest.cl/pin/491103534351777759/](https://www.pinterest.cl/pin/491103534351777759/)](Design%20for%20Personalized%20Fit%201c2469e866924f6eb4adb908398e9992/Untitled%2030.png)

[https://www.pinterest.cl/pin/491103534351777759/](https://www.pinterest.cl/pin/491103534351777759/)

1. **Personalization in Fit:** focuses on the interaction between the product, consumer, and its environment. Characteristics of the product such as shape, size, mass, colour palette, and personalized interactions (e.g. comfort) are adjusted to meet the individual’s needs.

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2031.png)

## Personalization in Fit

The following lesson will focus on *******************Personalization in Fit.******************* This design method relies on 3D scanning technology to capture precise measurements of the object or body part to be designed for and then uses algorithms to create custom patterns and shapes. The benefits of **********************Personalization in Fit********************** are numerous, including increased comfort, improved performance, and reduced waste. In this section, we will introduce you to the exciting world of personalized design and show you how to design your own personalized product using 3D scanning data with Rhino and Grasshopper.

# Selecting your Input Method

- There are various methods to create an input for your personalized design
    - Using a 3D scanner to create a 3D mesh
        - This can require to clean up the mesh to remove noise and unwanted objects
            - How can we do this in Grasshopper? I know we can do it in Blender or Meshmixer
        - We can use Smooth in Rhino or Smooth Mesh in Grasshopper to smoothed out the scan as well
        - Creating physical prototype based on a personalization and 3d scanning it
    - DINED database
        - how to access the data and what is available?
        - DINED plugin
    - Statistical Shape Modeling
        - Take multiple 3D scan samples and create statistically average models (or models in a certain percentile you want)
    - Take manual measurements of specific body locations or measurements with a machine

# Translating Body Data into Grasshopper Surface

## Outline

- There are many methods possible when creating personalized products for fit
    1. Turning a 3D scan mesh into a surface (covered in  [Lesson 4 - Surfaces](Grasshopper_Rhino_course/Lessons/4️⃣%20Lesson_4-Surfaces/!index.md))
        1. Create intersecting planes
        2. Find intersecting contour curves
        3. Loft the curves to create surface
    2. Example 1, but what happens with more complex scenarios
        1. Creating a surface from the fingers of the hands
        2. Creating a surface of the ear canal with its complex curves and structures
    3. Example 1, but instead creating physical prototype then 3d scanning and creating surface to add further design elements (mouse example)
    4. Having a fixed product design and then adapted to the 3d scan ([personalized glasses graduation project](https://repository.tudelft.nl/islandora/object/uuid%3A33a65390-41bb-4fb2-b2ac-7166fca7e87a?collection=education))
    5. Taking measurements to create custom shape ([low-cost foot scanner project](https://repository.tudelft.nl/islandora/object/uuid%3A0ee880fb-7063-42cd-aa82-b67f7c84d1e9?collection=education))
        1. Taking for example the creation of a custom shoe
        2. Take various measurements at fixed locations around the object
        3. Input these measurements into the Grasshopper script
        4. The measurements translate to the distance between certain points of the foot
        5. Curves are created around these points to form the contours
        6. A loft is created between these curves to form the foot shape

## Turning a 3D scan mesh into a surface (covered in  [Lesson 4 - Surfaces](Grasshopper_Rhino_course/Lessons/4️⃣%20Lesson_4-Surfaces/!index.md))

The first step in the design method is to create a surface from the imported 3D scan mesh. To learn more on this procedure, refer to Lesson 4 section creating surface

## Input 3D Scan Mesh

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2045.png)

## Find Bounding Box

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2046.png)

## Create Slicing Planes

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2047.png)

## Find Intersection Curves

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2048.png)

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2049.png)

- Curve needs to be rebuilt using “Rebuild Curve” component afterwards

## Create Loft from Curves

![Untitled](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Untitled%2050.png)

- Make sure Loft is Open

To create a loft from curves in Grasshopper, first find the intersection curves between the 3D scan mesh and the planes that were created along the model direction. Then, rebuild the curves using the "Rebuild Curve" component. Finally, create a loft from the curves using the "Loft" component, making sure that the loft is open.

## Fixed Product Personalized Design

Refer to [personalized glasses graduation project](https://repository.tudelft.nl/islandora/object/uuid%3A33a65390-41bb-4fb2-b2ac-7166fca7e87a?collection=education)

[Poster_VAN-WIJNGAARDEN_1528904.pdf.pdf](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Poster_VAN-WIJNGAARDEN_1528904.pdf.pdf)

![Screenshot 2023-04-03 at 10.38.09.png](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Screenshot_2023-04-03_at_10.38.09.png)

![Screenshot 2023-04-03 at 10.35.49.png](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Screenshot_2023-04-03_at_10.35.49.png)

![picture2_VAN-WIJNGAARDEN_1528904.jpg](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/picture2_VAN-WIJNGAARDEN_1528904.jpg)

## Taking Measurements to create custom shape

Refer to the following graduation project: [https://repository.tudelft.nl/islandora/object/uuid%3A0ee880fb-7063-42cd-aa82-b67f7c84d1e9?collection=education](https://repository.tudelft.nl/islandora/object/uuid%3A0ee880fb-7063-42cd-aa82-b67f7c84d1e9?collection=education)

![Screenshot 2023-03-31 at 12.09.08.png](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Screenshot_2023-03-31_at_12.09.08.png)

![Screenshot 2023-03-31 at 11.51.52.png](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Screenshot_2023-03-31_at_11.51.52.png)

![Screenshot 2023-03-31 at 11.51.04.png](Grasshopper_Rhino_course/Graduation_Projects/Design_for_Personalized_Fit/Screenshot_2023-03-31_at_11.51.04.png)

# Personalized Product Development - beyond the surface

## Outline

- After creating a surface in Grasshopper based on a body scan, a personalized product can now be created
- Personalization for aesthetics
    - The most basic computational method
    - Adding patterns to the design that serve simply for aesthetic value
    - Example with the arm cast
- Personalization based on data (see [Topic B - Data Driven Personalized Design](Grasshopper_Rhino_course/Graduation_Projects/Ergonomic_Data_Driven_Personalized_Design/!index.md))
    - Collect ergonomic data around the body part for used in the design
    - Examples of this include:
        - heat map data of the arm to improve heat comfort
        - Pressure data to create lattice structures for foot or seat comfort