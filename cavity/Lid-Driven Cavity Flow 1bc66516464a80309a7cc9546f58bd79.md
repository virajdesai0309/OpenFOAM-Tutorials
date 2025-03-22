# Lid-Driven Cavity Flow

# **Introduction** 🚀

Welcome to your first **OpenFOAM simulation**! 🎉 Today, we'll explore a classic computational fluid dynamics (CFD) problem: **Lid-Driven Cavity Flow**. By the end of this tutorial, you'll understand how to:

✅ Pre-process the simulation case
✅ Run the solver
✅ Post-process the results

Let's get started! 🔥

---

# **Problem Statement** 📌

In this tutorial, we will simulate **isothermal, incompressible flow** inside a **two-dimensional square domain**. The setup is as follows:

📌 **Domain Geometry:** A **square cavity** with all four boundaries as walls.
📌 **Boundary Conditions:**

- The **top wall** moves **horizontally (x-direction) at 1 m/s**.
- The **other three walls remain stationary**.

🔎 You can visualize the geometry in **Figure 2.1** [here](https://www.notion.so/Lid-Driven-Cavity-Flow-1bc66516464a80309a7cc9546f58bd79?pvs=21).

---

![2.1 Geometry of lid driven cavity](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image.png)

2.1 Geometry of lid driven cavity

## **⚙️ Pre-Processing**

Before running the simulation, we need to **set up the case files**.

### **📂 Locating the Case Files**

To access the required files, **navigate** to the OpenFOAM installation directory in **Linux Mint** or **search** for the following folder:

```bash
/opt/openfoam12/tutorials/incompressibleFluid/cavity
```

Once there, **copy the folder contents** to your OpenFOAM **working directory**:

```bash
cd $FOAM_RUN
```

💡 **Tip:** Use `ls` and `cd` commands to navigate!

---

## **🛠️ Mesh Generation**

OpenFOAM always operates in a **3D Cartesian coordinate system**. However, we can instruct it to solve a **2D case** by specifying a **special "empty" boundary condition** on patches normal to the **third dimension**.

### **📏 Mesh Details:**

- The cavity is a **square (0.1 m × 0.1 m) in the xy-plane**.
- A **uniform mesh (20 × 20 cells)** will be used.
- The mesh must be **one cell layer thick**, with **empty patches** on normal boundaries.

🖼️ **Mesh Structure:** The block structure is illustrated in **Figure 2.2**.

![Block Structure of the mesh cavity](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%201.png)

Block Structure of the mesh cavity

## **🛠️ Generating the Mesh**

To generate the mesh, let's open the **cavity folder** in **VS Code** or any code editor of your choice.

### **📂 Opening the File in VS Code**

1. **Launch VS Code** and open the **cavity folder**.
2. Open a **new terminal** inside VS Code.
3. Navigate to the `blockMeshDict` file inside the **system** folder.

💡 **Tip:** The file might look a bit overwhelming at first, but don’t worry! I've added comments inside for guidance.

### **🚀 Creating the Mesh**

Once inside the terminal, simply run the following command to generate the mesh:

```bash
blockMesh
```

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%202.png)

✅ **That's it!** You’ve now successfully created the block mesh. 🎉

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%203.png)

## **⚙️ Setting Up the Simulation**

### **📝 Boundary & Initial Conditions**

Now that we've generated the mesh, it's time to define the **boundary conditions**.

📂 **Where to Find Them?**

- Navigate to the `0` folder.
- Look for **pressure** (`p`) and **velocity** (`U`) files.

💡 **Tip:** Don't worry if it looks complex—I’ve added helpful comments inside the files!

---

### **⚗️ Defining Physical Properties**

After setting up boundary conditions, we need to define the **physical properties**.

📂 **Where to Find Them?**

- Head over to the `constant` folder.
- Locate the **`physicalProperties`** file.

🔍 **Explore & Modify:** The comments inside will guide you through any necessary changes!

---

### **📋 Simulation Control Settings**

To control how the simulation runs, we need to modify the **control settings**.

📂 **Where to Find Them?**

- Go to the `system` folder.
- Open the **`controlDict`** file.

📌 **What Does It Do?**

- Defines simulation **time steps**, **end time**, and **output intervals**.
- Adjust settings as needed!

---

## **🔍 Viewing the Mesh**

To check if the mesh was generated correctly, run the following command in the **VS Code terminal**:

```bash
paraFoam &
```

💡 **Tip:** This will launch **ParaView**, a tool for visualizing OpenFOAM simulations.

---

## **🏃 Running the Simulation**

Now, let's **execute the simulation**! 🚀

In the **VS Code terminal**, type:

```bash
foamRun
```

📌 **What Happens Next?**

- OpenFOAM will start solving the equations.
- New folders (`0.5, 1.0, 1.5, 2.0, ...`) will be created inside the `cavity` folder, storing results at different time steps.

---

## **📊 Post-Processing & Results**

Once the simulation is complete, we can **view the results** in ParaView.

1️⃣ Open ParaView by running:

```bash
paraFoam &
```

2️⃣ **In ParaView:**

- Click **Apply** to visualize the results.
- Explore the velocity field, pressure distribution, and flow patterns.

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%204.png)

### **🎥 Running the Animation**

1️⃣ In **ParaView**, locate the **Properties Panel** on the left.

2️⃣ Find and **select** `U` (**velocity field**) from the **list of variables**.

3️⃣ Click on the **Play ▶️** button to animate the simulation! 🎬

---

### **🎨 Adjusting the Color Map**

To improve visualization clarity:

1️⃣ **Go to** `View` → `Color Map Editor` in the menu ribbon.

2️⃣ Locate the **Color Discretization** setting.

3️⃣ **Change it from** `256` **to** `12`.

✅ This makes the velocity gradient **easier to interpret**!

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%205.png)

### **🛠️ Activating Start Trace in ParaView**

To **record your actions** for reproducibility, you can activate the **Start Trace** feature in ParaView. This will log every step you take, making it easier to **automate post-processing** in the future!

### **📌 How to Enable Start Trace**

1️⃣ In **ParaView**, go to **`Tools` → `Start Trace...`**

2️⃣ A new **Trace Options** window will pop up.

3️⃣ Select the following options:

- **Properties Modified**: ✅ *(Only log changes you make)*
- **Fully Traceable State**: ✅ *(Captures everything, useful for scripting)*
    
    4️⃣ Click **OK** to start recording your actions.
    

🔴 **Now, every click and change you make will be logged.**

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%206.png)

### **📏 Creating a 2D Slice View in ParaView**

To **reduce the 3D view to a 2D slice**, follow these steps:

### **🔍 Finding the Slice Tool**

1️⃣ Press **`CTRL + Spacebar`** to open the **Find** search bar.

2️⃣ Type **"Slice"** and select the **Slice** filter.

3️⃣ Click **OK** or press **Enter** to activate the tool.

---

### **✂️ Slicing Along the Z-Axis**

1️⃣ In the **Properties Panel**, locate the **Slice Normal** settings.

2️⃣ Set the **normal direction** to **Z-axis** (`0, 0, 1`).

3️⃣ Click **Apply** to generate the **2D slice** view.

✅ You now have a **2D representation** of the velocity and pressure fields! 🎉

Would you like to overlay **streamlines** for better visualization? 🚀

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%207.png)

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%208.png)

### **🎨 Enhancing the Slice View with Turbo Colormap**

To improve visualization, let's apply the **Turbo** colormap to the slice view.

### **🖌️ Changing the Colormap**

1️⃣ **Open** the **Color Map Editor**:

- Click on **`View` → `Color Map Editor`** in the menu ribbon.

2️⃣ **Select the Slice View** in the **Pipeline Browser** (if not already selected).

3️⃣ In the **Color Map Editor**, locate the **colormap dropdown menu**.

4️⃣ Scroll through the list and **select** **`Turbo`** for a more vibrant and intuitive visualization.

5️⃣ Click **Apply** to update the colors in the slice view.

✅ **Done!** You now have a **visually enhanced 2D slice** using the Turbo colormap. 🎨🔥

Would you like to add **contours** or **streamlines** next for better flow visualization? 🚀

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%209.png)

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2010.png)

### **🔍 Adding Contours to the Visualization**

Now, let's overlay **contours** to highlight specific velocity or pressure levels!

### **📌 Finding the Contour Tool**

1️⃣ Press **`CTRL + Spacebar`** to open the **Find** search bar.

2️⃣ Type **"Contour"** and select the **Contour** filter.

3️⃣ Press **Enter** or click **OK** to activate it.

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2011.png)

### **⚙️ Setting Up Contours**

1️⃣ In the **Properties Panel**, locate the **Contour By** dropdown menu.

2️⃣ Choose **`U` (Velocity)** or **`p` (Pressure)** as the variable to contour.

3️⃣ Set the **Contour Levels**:

- Click **Add Range** to specify multiple levels, or
- Manually enter values based on the velocity/pressure range.

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2012.png)

4️⃣ Click **Apply** to generate the contours.

✅ **Done!** You now have a clear view of flow patterns with contour lines! 🎯

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2013.png)

### **👀 Managing Views in ParaView**

💡 **Tip:** Click on the **eye 👁️ symbol** next to each view in the **Pipeline Browser** to **enable or disable** different visualizations. This helps in focusing on specific results without clutter.

---

### **🎯 Adding Glyphs for Vector Visualization**

Now, let's add **glyphs** to visualize velocity vectors!

### **📌 Finding the Glyph Tool**

1️⃣ **Select the Slice View** in the **Pipeline Browser**.

2️⃣ Press **`CTRL + Spacebar`** to open the **Find** search bar.

3️⃣ Type **"Glyph"** and select the **Glyph** filter.

4️⃣ Press **Enter** or click **OK** to activate it.

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2014.png)

### **⚙️ Configuring Glyphs (Vector Arrows)**

1️⃣ In the **Properties Panel**, locate the **Glyph Type** dropdown.

2️⃣ Choose **Arrow** (or another suitable shape like Hedgehog).

3️⃣ Set the **Glyph Scale** to adjust arrow sizes for better visibility.

4️⃣ Choose **`U` (Velocity Field)** as the input data.

5️⃣ Click **Apply** to generate velocity vectors.

✅ **Done!** Now you can see **velocity vectors** overlaid on the slice view! 🏹

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2015.png)

### **🌊 Adding Streamlines for Flow Visualization**

Now, let's visualize the **flow paths** using the **Stream Tracer** tool!

### **🔍 Finding the Stream Tracer Tool**

1️⃣ **Select the Slice View** in the **Pipeline Browser**.

2️⃣ Press **`CTRL + Spacebar`** to open the **Find** search bar.

3️⃣ Type **"Stream Tracer"** and select the **Stream Tracer** filter.

4️⃣ Press **Enter** or click **OK** to activate it.

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2016.png)

### **⚙️ Configuring Streamlines**

1️⃣ **Adjust the Arrow Position & Orientation** as per your visualization needs.

2️⃣ Locate the **Resolution** setting in the **Properties Panel**.

3️⃣ Reduce the **Resolution** from **256** to **21** for a more optimized view.

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2017.png)

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2018.png)

4️⃣ Click **Apply** to generate the streamlines.

✅ **Done!** You now have **streamlines** representing the flow paths in your simulation! 🔥

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2019.png)

### **🌀 Enhancing Streamlines with Tubes**

Now, let's make the **streamlines more visible** by applying a **Tube Filter**!

### **🔍 Finding the Tube Filter**

1️⃣ **Select the `Stream Tracer` filter** in the **Pipeline Browser**.

2️⃣ Press **`CTRL + Spacebar`** to open the **Find** search bar.

3️⃣ Type **"Tube"** and select the **Tube** filter.

4️⃣ Press **Enter** or click **OK** to activate it.

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2020.png)

### **⚙️ Adjusting Tube Settings**

1️⃣ **Locate the `Tube Radius`** setting in the **Properties Panel**.

2️⃣ **Reduce the tube radius** as per your needs to avoid excessive thickness.

3️⃣ Click **Apply** to generate the **smooth, 3D-enhanced streamlines**.

✅ **Done!** Your streamlines now appear as smooth, tubular structures for better clarity! 🎯

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2021.png)

### **🛠️ Saving the Trace**

After making adjustments (e.g., selecting velocity, playing animation, changing color discretization):

1️⃣ Go to **`Tools` → `Stop Trace`**

2️⃣ A Python script will be generated with all your recorded steps.

3️⃣ Click **Save As** and store it for future automation!

✅ **This is useful if you want to automate post-processing with Python in ParaView!**

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2022.png)

### **💾 Saving the Script as a Macro in ParaView**

To **automate** the entire visualization process, let's save this sequence as a **Macro** in ParaView! This will allow you to quickly generate the plots in future simulations **without repeating the steps manually**.

![image.png](Lid-Driven%20Cavity%20Flow%201bc66516464a80309a7cc9546f58bd79/image%2023.png)

### **🛠️ Using the Macro**

✅ Next time you need to generate the same plots, simply:

- Open your simulation results in ParaView.
- Go to **`Macros`** in the menu bar.
- Click on **`LidDrivenCavityMacro`** to apply all the visualization steps instantly! 🚀

## References

https://www.openfoam.com/documentation/tutorial-guide/2-incompressible-flow/2.1-lid-driven-cavity-flow#x6-60002.1

https://docs.paraview.org/en/latest/Tutorials/ClassroomTutorials/beginningSourcesAndFilters.html#slice-filter

https://docs.paraview.org/en/latest/Tutorials/ClassroomTutorials/beginningSourcesAndFilters.html#glyph-filter

https://docs.paraview.org/en/latest/Tutorials/ClassroomTutorials/beginningSourcesAndFilters.html#contour-filter

https://docs.paraview.org/en/latest/Tutorials/ClassroomTutorials/beginningSourcesAndFilters.html#stream-tracer

https://docs.paraview.org/en/latest/Tutorials/ClassroomTutorials/beginningColorMapsAndPalettes.html#color-map-editor