# Experiment 4 — Physical Design of a 4-Bit Up-Down Counter

## Aim

Execute floorplanning, power planning, and placement for the synthesised 4-bit up-down counter design.

## Tool Required

**Physical Design:** Innovus

---

## Mandatory Inputs for PD

1. **Gate Level Netlist** — Output of Synthesis
2. **Block Level SDC** — Output of Synthesis
3. **Liberty Files** — `.lib`
4. **LEF Files** — Layer Exchange Format

---

# Procedural Steps

Ensure the Synthesis for the target design is complete, and then open a terminal from the corresponding workspace.

* Initiate the Cadence tools and cmd: `innovus` (Press Enter).
* For Innovus tool, a GUI opens, and the terminal also enters the Innovus command prompt, where the tool commands can be entered.

After importing the Design, perform the following Physical Design stages:

<img width="1600" height="900" alt="image" src="https://github.com/user-attachments/assets/6a006143-439d-4252-9c01-a7ff2b2c1590" />

> **Floor Planning → Power Planning → Placement**

**Note:** Check the paths to properly read in the input files.

---

## Importing the Design Using GUI

Else, if you would like to import your design using GUI, open the Innovus tool and from the GUI, go to:

**File → Import Design**

A new pop-up window appears.

### Loading the Netlist

<img width="938" height="592" alt="image" src="https://github.com/user-attachments/assets/064addc8-9838-4a57-ac41-2534d060eb70" />

* First, load the netlist.
* You can browse for the file and select **“Top cell: Auto Assign”**.

### Loading LEF Files

<img width="722" height="467" alt="image" src="https://github.com/user-attachments/assets/62ce6175-2aad-4864-a067-85bdffcfb3b2" />

* Similarly, select your LEF files from the specified path.
* Once LEF Files are loaded, the next step is to create the power supply pins both **VDD** and **VSS**.

---

# Creating Delay Corners and Analysis View

In order to load the Liberty File and SDC, create delay corners and analysis view, select the **“Create Analysis Configuration”** option at the bottom.

<img width="777" height="164" alt="image" src="https://github.com/user-attachments/assets/1b68a9f7-35b8-4e15-8e74-88de1a24f2a5" />


A **MMMC browser** pops up.

![MMMC Browser](https://github.com/user-attachments/assets/12b66c0e-44d0-437e-878e-7620932e7edd)

### Order of Adding MMMC Objects

The order of adding the MMMC Objects is as follows:

1. **Library Sets**
2. **RC Corners**
3. **Delay Corners**
4. **Constraints (SDC)**

Once all of them are added, Analysis Views are created and assigned to **Setup** and **Hold**.

To add any of the objects:

**Right-click on the corresponding label → Select New**

---

## 1. Adding Liberty Files

Add `slow.lib` and `fast.lib` under **Library Sets**.

### Adding `slow.lib`

* Add `slow.lib` with a label **Slow** or any identifier of your own.

<img width="754" height="476" alt="image" src="https://github.com/user-attachments/assets/69d07102-c10a-42f2-9bdf-804484415118" />

**Fig. 1 — Add slow Library set**

### Adding `fast.lib`

* Add `fast.lib` with a label **Fast** or any identifier of your own.
  
<img width="942" height="592" alt="image" src="https://github.com/user-attachments/assets/ba3f3084-dc2b-49cc-8e42-105c0f29a927" />

**Fig. 2 — Add fast Library set**

---

## 2. Adding RC Corners

Adding RC Corners can also be done in a similar process.

* The temperature value can be found under the corresponding liberty file.
* Also, cap table and RC Tech files can be added from Foundry where available.

<img width="453" height="376" alt="image" src="https://github.com/user-attachments/assets/b477b69e-d39a-4306-a4ef-bfa0aa2ee135" />

**Fig. 3 — Add RC corner**

---

## 3. Adding Delay Corners

Delay Corners are formed by combining **Library Sets** with **RC Corners**.
<img width="620" height="575" alt="image" src="https://github.com/user-attachments/assets/adc0e473-c867-44ad-9e03-a41b116e5f1e" />

**Fig. 4 — Add Delay corner Max_delay & Min_delay**

---

## 4. Adding Constraints (SDC)

Similarly, SDC can be read under the MMMC Object of **“Constraints”**.

<img width="935" height="591" alt="image" src="https://github.com/user-attachments/assets/963b1046-6994-425d-9417-59c2c3655a46" />

**Fig. 5 — SDC Constraint file**

---

## 5. Creating Analysis Views

Analysis Views are formed from combinations of **SDC** and **Delay Corner**.

<img width="750" height="234" alt="image" src="https://github.com/user-attachments/assets/30c8d45d-0487-4f53-bcd1-765d2155672c" />
<img width="751" height="216" alt="image" src="https://github.com/user-attachments/assets/69ca1129-6e1a-4bb0-904d-41a57845ca59" />

**Fig. 6 — Add Analysis view Worstcase & Bestcase**

Once **“Best”** and **“Worst”** Analysis views are created, assign them to **Setup** and **Hold**.
<img width="752" height="182" alt="image" src="https://github.com/user-attachments/assets/eed05443-5145-4ee9-bac8-88fa65d0267d" />
<img width="726" height="181" alt="image" src="https://github.com/user-attachments/assets/5214e78f-d035-4ce1-970b-3b8433846541" />

**Fig. 7 — Add Setup Analysis View & Hold Analysis View**

---

## Saving the MMMC Configuration

Once all the process is done:

* Click **“Save & Close”**.
* Save the script generated with any name of your choice.
* Make sure the file extension remains `.view` or `.tcl`.

After saving the script, go back to **Import Design** window and click **“OK”** to load your design.

![Import Design](https://github.com/user-attachments/assets/9daa96ae-ee07-42a3-804a-58f68763fd55)

In the Import Design window click the **save** option to save the `Default.globals` file.

---

# Core Area

A rectangular or square box appears in your GUI if and only if all the inputs are read properly.

<img width="1600" height="898" alt="image" src="https://github.com/user-attachments/assets/8a3f6221-afc5-4abf-a646-aa89fc6d65e1" />

**Fig. 8 — Core area**

* The internal area of the box is called **“Core Area”**.
* The horizontal lines running along the width of Core are **“Standard Cell Rows”**.
* Every alternate of them are marked indicating alternate **VDD** and **VSS** rows.
* This setup is called **“Flipped Standard Cell Rows”**.

---

# Floorplan

## Steps under Floorplan

1. **Aspect Ratio**
   Ratio of Vertical Height to Horizontal Width of Core

2. **Core Utilisation**
   The total Core Area % to be used for Floor Planning

3. **Channel Spacing**
   Channel Spacing between Core Boundary to IO Boundary

Select:

**Floorplan → Specify Floorplan**

to modify/add concerned values to the above Factors.

On adding/modifying the concerned values, the core area is also modified.

<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/931e5c9f-5464-4b50-85c9-85c5e3d9b743" />

**Fig. 9 — Specify Floorplan**

The Yellow patch on the Left Bottom are the group of **“Unassigned pins”** which are to be placed along the IO Boundary along with the Standard Cells [Gates].

---

# Power Planning

## Steps under Power Planning

1. **Connect Global Net Connects**
2. **Adding Power Rings**
3. **Adding Power Strings**
4. **Special Route**

---

## 1. Connect Global Net Connects

Under Connect Global Net Connects, we create two pins, one for **VDD** and one for **VSS** connecting them to corresponding Global Nets as mentioned in Globals file / Power and Ground Nets.

1. Select **Power → Connect Global Nets..** to create **“Pin”** and **“Connect to Global Net”** as shown and use **“Add to list”**.
2. Click on **“Apply”** to direct the tool in enforcing the Pins and Net connects to Design and then Close the window.

---

## 2. Adding Power Rings and Power Stripes

In order to tap in Power from a distant Power supply, Wider Nets and Parallel connections improve efficiency.

Moreover, the cells that would be placed inside the core area are expected to have shorter Nets for lower resistance.

Hence **Power Rings [Around Core Boundary]** and **Power Stripes [Across Core Boundary]** are added which satisfies the above conditions.

### Adding Power Rings

Select:

**Power → Power Planning → Add Rings**

to add Power rings **‘around Core Boundary’**.

* Select the Nets from Browse option **OR**
* Directly type in the Global Net Names separated by a space being Case and Spelling Sensitive.
* Select the Highest Metals marked **‘H’ [Horizontal]** for Top and Bottom and Metals marked **‘V’ [Vertical]** for Right and Bottom.
* This is because Highest metals have Highest Widths and thus Lowest Resistance.
* Click on **Update** after the selection and **“Set Offset: Centre in Channel”** in order to get the Minimum Width and Minimum Spacing of the corresponding Metals and then Click **“OK”**.

### Adding Power Stripes

Similarly, Power Stripes are added using similar content to that of Power Rings.

On adding Power Stripes, The Power mesh setup is complete as shown.

However, there are no Vias that could connect Metal 9 or Metal 8 directly with Metal 1 [VDD or VSS of Standard Cells are generally made up of Metal 1].

---

## 3. Special Route

The connection between the Highest and Lowest Metals is done through **Stacking of Vias** done using **“Special Route”**.

To perform Special Route:

**Route → Special Route → Add Nets → OK**

After the Special Route is complete, all the Standard Cell Rows turn to the Color coded for Metal 1.

<img width="1021" height="895" alt="image" src="https://github.com/user-attachments/assets/fd807564-59ef-458e-9fe7-cca0e1640164" />

**Fig. 10 — Power plan**

The complete Power Planning process makes sure Every Standard Cell receives enough power to operate smoothly.

---

# Placement

1. The Placement stage deals with Placing of **Standard Cells** as well as **Pins**.

2. Select:

   **Place → Place Standard Cell → Run Full Placement → Mode → Enable ‘Place I/O Pins’ → OK → OK**

All the Standard Cells and Pins are placed as per the communication between them, i.e., Two communicating Cells are placed as close as possible so that shorter Net lengths can be used for connections as Shorter Net Lengths enable Better Timing Results.

<img width="1600" height="897" alt="image" src="https://github.com/user-attachments/assets/6e170e93-9330-4852-839e-0fcc9daa226e" />

**Fig. 11 — Placement of standard Cells**

You can toggle the Layer Visibility from the list on the Right.

The List of Layers available are shown on the right under **“Layer”** tab with colour coding.

---

# Result

Thus, the physical design stages up to placement for the **4-bit up-down counter** were completed and verified.
