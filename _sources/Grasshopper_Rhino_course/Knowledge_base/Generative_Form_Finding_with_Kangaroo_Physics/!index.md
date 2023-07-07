# Generative Form Finding with Kangaroo Physics

Categories: Lesson
Created: April 20, 2023 11:57 PM
Review: Currently Working On
Tags: Form Finding, Generative, Simulation

📌 ********************Outlines:******************** A short description of what you can expect in the upcoming section.
📑 **Explanation text:** Written explanations with supporting images.
👩‍🏫 ************************************Explanation videos:************************************ Explaining the course material in short lecture videos.
📺 **Tutorial videos:** Follow-along tutorials.
💡 T********************ips:******************** Tips and tricks to make working in Rhino/Grasshopper easier.
🖱️ **Exercises:** Small practice questions. The solution is provided.
💻 **Assignments:** Open-ended assignments, to practice further with the course materials.

# Outline

- introduction into Grasshopper Kangaroo physics
- Basics of setting up kangaroo in Grasshopper
- Example show case
    - Creating a textile 3d structure
    - Creating a textile 3d tent
    - Creating a 4d printed textile shape change simulation
    - Creating a growing pattern on a vase
- Case study for personalized design
- Future work
- Related works

# Introduction

This tutorial focuses on using Kangaroo physics simulations in Grasshopper to create generative geometry. In this tutorial, we will discuss the basics of physics simulation and how it can be used to create generative geometry. We will go over the necessary components needed to set up a Kangaroo simulation and how to set up constraints and goals for the simulation to achieve the desired outcome.

Learning Kangaroo physics simulations in Grasshopper provides a new computational thinking model for creating generative geometry. This can be useful for a wide range of applications, from architecture and product design to art and sculpture. Kangaroo simulations can be also be used to model complex physical phenomena, such as the behavior of textiles or the growth of natural systems. This can provide insights that might be difficult or impossible to obtain through other means. 

# Basics

In this section, we will learn how to set up Kangaroo in Grasshopper. Kangaroo requires a different way of thinking than the traditional Grasshopper workflow. With Kangaroo, we use what are called “Goals” to define the various forces and constraints acting on the geometry during the Kangaroo simulation. Additionally, the designer must be careful on optimizing the input geometry to ensure the simulation runs effectively as it can be a computationally intensive task.

To set up a Kangaroo simulation in Grasshopper, the general steps are as follows:

1. Prepare the input geometry
    1. We need to use meshes, where the resolution of the mesh defines the resolution of the simulation
2. Decide on the physical constraints that will be applied to the system
    1. Deciding which parts of the geometry will be fixed, which will be flexible, where the forces will be applied, etc
    2. Based on this, we need to isolate the different parts of the geometry such as the main mesh, edges of the mesh,etc
3. Apply Kangaroo Goals components to the parts of the geometry to assign constraints
4. Use the Show component to select which geometry to show in the output
5. Set up Kangaroo solver
    1. Merge all the Goal components
    2. Make sure to add reset and toggle on/off button to the simulation
6. Run the simulation 
7. Adjust Goal parameters or resolution of components to obtain desired results

Take a look at the example showcase where we discuss different potential application cases of generating geometry with Kangaroo to learn how to set up typical Kangaroo scripts.

# Example Showcase

This section demonstrates several examples, including:

- Creating a textile 3D structure.
- Creating a textile 3D tent.
- Creating a 3D printed textile shape change simulation.
- Creating a growing pattern on a vase.

# Creating an Organic Cross Structure

[GenerativeMesh](GenerativeMesh.gh)

![Untitled](Untitled.gif)

To create a an Organic Cross Structure using Grasshopper Kangaroo physics simulations, the following steps should be followed.

Firstly, open the [GenerativeMesh.gh](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2dfd458e-61ab-40f4-b814-59f92c887dcb/GenerativeMesh.gh) file. This file contains the Grasshopper definition that demonstrates how to create the structure.

Secondly, to create the mesh used for the simulation, we need to convert our surface into a mesh and decide on the necessary mesh resolution to optimally run the simulation. This mesh will be used in the simulation.

Thirdly, create flexible edges of the mesh using the "Edge Length" component. This component is used to create a force that can keep the edges of the mesh within a certain length, allowing it to bend and fold while still maintaining its shape.

Fourthly, fix the edges of the mesh using an "Anchor" component. This component is used to fix the edges of the mesh to certain points, ensuring that they do not move during the simulation.

Fifthly, use a "Show" component to output the mesh. This component is used to display the mesh during the simulation.

The next step is to load the mesh onto the Kangaroo solver. This is done by connecting the Kangaroo components to the "Kangaroo Solver" component. The "Kangaroo Solver" component is used to run the simulation and update the geometry in real-time. By following these steps, a textile 3D structure as shown in the example image can be created.

It is important to note that these steps provide a general overview of how to set up a Kangaroo simulation in Grasshopper. Additionally, the simulation parameters can be adjusted to achieve different results. For example, the strength of the forces, the number of iterations, or other simulation parameters can be adjusted to achieve the desired outcome.

![Untitled](Untitled.png)

# Creating a Textile 3D tent

[Generative Tent.gh](Generative_Tent.gh)

![Screen-Recording-2023-06-02-at-16.44.21](Screen-Recording-2023-06-02-at-16.44.21.gif)

![Screenshot 2023-06-02 at 16.35.00.png](Screenshot_2023-06-02_at_16.35.00.png)

# Creating a 4D-printed Shape Changing Textile

[Programmable Textile.gh](Programmable_Textile.gh)

![textile1374-1480](textile1374-1480.gif)

![ezgif.com-optimize](ezgif.com-optimize.gif)

![Screenshot 2023-06-02 at 17.22.59.png](Screenshot_2023-06-02_at_17.22.59.png)

![Screenshot 2023-06-02 at 17.18.57.png](Screenshot_2023-06-02_at_17.18.57.png)

# Creating a growing pattern on a vase

[Generative Grow on Vase.gh](Generative_Grow_on_Vase.gh)

![Screen Recording 2023-06-02 at 17.51.50 (4).gif](4).gif).gif).gif)

![Screenshot 2023-06-02 at 17.43.46.png](Screenshot_2023-06-02_at_17.43.46.png)

# Case Study: Personalized Design from 3D Scan using Kangaroo Physics

[Generating a Mesh from Ear Canal Cavity (Kangaroo Physics).gh](Kangaroo%20Physics).gh).gh).gh)

For more complicated 3D scan geometry, the approached mentioned above might not be sufficient to generate good results. In this cases, a more creative approach is necessary. Let's take for example, the geometry of an ear canal. in this scenario, we would like to create an earbud that is personalized for the user's 3D scan and perfectly fits the cavity of the ear canal.

One approach we can take is to use Grasshoppers Kangaroo physics simulation to generate the geometry of the earbud. It is important to note that the following approach is for advanced users, only works on Windows PC for now, and requires the following plugins:

- Weaverbird
- Lunchbox
- Pufferfish
- Dendro

If you are new to Grasshopper Kangaroo physics simulation, it is recommended to first read the lesson on (Insert link to Form Finding with Kangaroo Physics). This approach is as follows:

1. Simplify the geometry of the ear to speed up the simulation

![Untitled](../../Graduation%20Projects/Design%20for%20Personalized%20Fit/Untitled%2018.png)

![Untitled](../../Graduation%20Projects/Design%20for%20Personalized%20Fit/Untitled%2019.png)

1. Prepare a distribution of small spheres to collide with the ear canal and set up the simulation with Kangaroo

![Untitled](../../Graduation%20Projects/Design%20for%20Personalized%20Fit/Untitled%2020.png)

1. Run the simulation allowing the spheres to collide with the ear and fill up the ear canal cavity

![Untitled](../../Graduation%20Projects/Design%20for%20Personalized%20Fit/Untitled%2021.png)

![Untitled](../../Graduation%20Projects/Design%20for%20Personalized%20Fit/Untitled%2022.png)

1. Create a volume from the collection of spheres and convert into mesh

![Untitled](../../Graduation%20Projects/Design%20for%20Personalized%20Fit/Untitled%2023.png)

![Untitled](../../Graduation%20Projects/Design%20for%20Personalized%20Fit/Untitled%2024.png)

For more details on this implementation, refer to the example file provided: [Generating a Mesh from Ear Canal Cavity (Kangaroo Physics)](Kangaroo%20Physics))). In this approach, we can adjust the size and shape of the final mesh by adjusting the simulation parameters. For example, if we want the earbud to cover a larger area of the ear, then we can add more balls to the simulation to increase the total area covered by the balls. Experiment with the example file and test it out for yourself!

# Related Works

[Untitled Database](Untitled%20Database.csv)