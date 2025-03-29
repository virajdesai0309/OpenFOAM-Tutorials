# Lid Driven Cavity Flow With Fine Mesh

# 🔥 Refining the Cavity Flow Simulation with a Finer Mesh! 🏁

Now that our cavity flow model is ready, let's take it up a notch! 🚀 We're going to **increase the mesh resolution** and see how the results improve. More mesh points = better accuracy! ✅

### 🎯 What’s the Plan?

- **Double the mesh density** in each direction 📈
- **Map** the results from the coarser mesh onto the finer one 🗺️
- **Compare** the refined simulation with the original ⚖️

---

## 🏗️ Creating a New Case from an Existing One

To create a new case from the existing one, you can **copy the folder manually** or use these simple commands in the CLI:

```bash
cd $FOAM_RUN
cd cavity
```

This lands you inside the **cavity** case folder. Now, let’s create a new directory for the finer mesh:

```bash
cd ..
mkdir cavityFine
```

Next, **copy the essential files** into the new folder:

```bash
cp -r cavity/constant cavityFine
cp -r cavity/system cavityFine
cd cavityFine
```

---

## 🛠️ Creating a Finer Mesh

To refine our mesh, we’ll edit the **blockMeshDict** file. Open it in your favorite text editor (I’ll use VS Code, but you can use any! 📝).

📌 **Original mesh size:** (20,20,1)
📌 **New refined mesh size:** (40,40,1)

After updating the file, save it and **run the following command** to generate the finer mesh:

```bash
blockMesh
```

The output would be a geometry with 1600 nodes (40x40x1)

```bash
/*---------------------------------------------------------------------------*\
  =========                 |
  \\      /  F ield         | OpenFOAM: The Open Source CFD Toolbox
   \\    /   O peration     | Website:  https://openfoam.org
    \\  /    A nd           | Version:  12
     \\/     M anipulation  |
\*---------------------------------------------------------------------------*/
Build  : 12-86e126a7bc4d
Exec   : blockMesh
Date   : Mar 26 2025
Time   : 10:41:16
Host   : "viraj-Lenovo-ideapad-320-15IKB"
PID    : 17625
I/O    : uncollated
Case   : /home/viraj/OpenFOAM/viraj-12/run/cavityFine
nProcs : 1
sigFpe : Enabling floating point exception trapping (FOAM_SIGFPE).
fileModificationChecking : Monitoring run-time modified files using timeStampMaster (fileModificationSkew 10)
allowSystemOperations : Allowing user-supplied system call operations

// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //
Create time

Deleting polyMesh directory
    "/home/viraj/OpenFOAM/viraj-12/run/cavityFine/constant/polyMesh"
Reading "blockMeshDict"

Creating block mesh from
    "system/blockMeshDict"
No non-linear block edges defined
No non-planar block faces defined
Creating topology blocks
Creating topology patches

Creating block mesh topology

Check topology

        Basic statistics
                Number of internal faces : 0
                Number of boundary faces : 6
                Number of defined boundary faces : 6
                Number of undefined boundary faces : 0
        Checking patch -> block consistency

Creating block offsets
Creating merge list .

Creating polyMesh from blockMesh
Creating patches
Creating cells
Creating points with scale 0.1
    Block 0 cell size :
        i : 0.0025 .. 0.0025
        j : 0.0025 .. 0.0025
        k : 0.01

No patch pairs to merge

Writing polyMesh
----------------
Mesh Information
----------------
  boundingBox: (0 0 0) (0.1 0.1 0.01)
  nPoints: 3362
  nCells: 1600
  nFaces: 6480
  nInternalFaces: 3120
----------------
Patches
----------------
  patch 0 (start: 3120 size: 40) name: movingWall
  patch 1 (start: 3160 size: 120) name: fixedWalls
  patch 2 (start: 3280 size: 3200) name: frontAndBack

End
```

## 🔄 Mapping the Coarse Mesh Results to the Fine Mesh

The `mapFields` utility helps us transfer results from one mesh to another. Since the **geometry and boundary conditions are identical**, we’ll use the `-consistent` option:

```bash
mapFields ../cavity -consistent
```

📝 **Pro Tip:** Set `startTime` to `0.5 s` in `controlDict` before running this command!

The output would be 

```bash
/*---------------------------------------------------------------------------*\
  =========                 |
  \\      /  F ield         | OpenFOAM: The Open Source CFD Toolbox
   \\    /   O peration     | Website:  https://openfoam.org
    \\  /    A nd           | Version:  12
     \\/     M anipulation  |
\*---------------------------------------------------------------------------*/
Build  : 12-86e126a7bc4d
Exec   : mapFields ../cavity -consistent
Date   : Mar 26 2025
Time   : 10:43:13
Host   : "viraj-Lenovo-ideapad-320-15IKB"
PID    : 17754
I/O    : uncollated
Case   : /home/viraj/OpenFOAM/viraj-12/run/cavityFine
nProcs : 1
sigFpe : Enabling floating point exception trapping (FOAM_SIGFPE).
fileModificationChecking : Monitoring run-time modified files using timeStampMaster (fileModificationSkew 10)
allowSystemOperations : Allowing user-supplied system call operations

// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //
Source: "/home/viraj/OpenFOAM/viraj-12/run" "cavity"
Target: "/home/viraj/OpenFOAM/viraj-12/run" "cavityFine"

Create databases as time

Source time: 0.5s
Target time: 0.5s
Create meshes

Source mesh size: 400   Target mesh size: 1600

Consistently creating and mapping fields for time 0.5

    interpolating p
    interpolating nut
    interpolating k
    interpolating epsilon
    interpolating U

End
```

## 🎛️ Adjusting Simulation Controls ⚙️

Since we halved the cell size, we also need to **halve the time step** to keep the **Courant number** below 1. Update `controlDict` as follows:

🔹 `deltaT` → `0.0025 s`

🔹 `writeInterval` → `0.1`

🔹 `writeControl` → `runTime`

Save your changes! 🖫

---

## 🚀 Running the Simulation as a Background Process

Let’s run the case in the background so we can check the output later. From the `cavityFine` directory, execute:

```bash
foamRun > log &
cat log
```

The output will be 

```bash
[1] 17838
```

✅ This way, you can monitor the progress while doing other tasks!

---

## 📊 Post-Processing with ParaView 🎨

To visualize the results, type:

```bash
paraFoam &
```

Now, let’s **compare** with the original **cavity case**:

```bash
cd ../cavity
paraFoam -touch
ls
```

This creates a new file `cavity.OpenFOAM`. Open **ParaView**, navigate to the file, and **click Apply**! ✅ If you created a macro in the previous tutorial, run it to get quick insights! 🎥

![image.png](Lid%20Driven%20Cavity%20Flow%20With%20Fine%20Mesh%201c266516464a80e68f3ed275c0cfe1ea/image.png)

## 🎥 Arranging the Side View in RenderView2

1. Click on the **🖼 RenderView2** option to enable the **vertical layout**.
2. Arrange the models as follows:
    - **⬅️ Left Side**: Model with a **higher mesh density**.
    - **➡️ Right Side**: Model with a **lower mesh density**.
3. Set the parameter to **⚡ Velocity** and choose **📏 Surface with Edges**.
4. Click the **▶️ Play** button to view the animation in a side-by-side comparison.

 

![Comparision of animation.gif](Lid%20Driven%20Cavity%20Flow%20With%20Fine%20Mesh%201c266516464a80e68f3ed275c0cfe1ea/Comparision_of_animation.gif)