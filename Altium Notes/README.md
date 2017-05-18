Altium Designer Notes
=====================

# Creating Parts
 - Add supplier data into schematic symbol using supplier search.
 - Hide supplier part number.
 - Draw the symbol.
 - Change designator.
 - change default comment to manufacture part number.
 - Change mouse settings to match that of kicad.
 - Draw body outline, adding the tolerances in data-sheet.
 - Get 3D models from 3d central.
 -  Use layer 29 for assembly drawing. Add indication for pin 1 and add designator.
 - Update schematic symbol after making any needed changed in the symbol.
 - Add snap point for 3D model to accurately place on the foot print.

## Tips
 - Single layer mode Shift+S
 - In PCB and Foot print scope press Q to change grid from mil to mm.
 - Use sch filter and inspector to select objects by type and change properties in selection group.
 - Create notes in schematics.
 - Use sch navigator to browse the sch by going through all the nets and make sure its correct.
 - Add pcb and firmware in the schematic.
 - Create custom Title block and custom BOM template. Use parameters for text in title block
 - Change undo/redo stack to 1000 in both schematic and pcb
 - In project options disable rooms.
 - Add notes with colour code and titles in schematic and provide legend on cover page.
 - Use two monitor setup, one with schematic and one with pcb.
 - Enable Tools> Cross select mode
 - Press R while moving component to change modes(Avoid, Push, Ignore)
 - After selecting component in schematic after Cross probing, the mask in pcb goes away. To fix this, right click on navigator and select "Select Objects".
 - CTRL + Click on net to highlight it. use '[' and ']' change intensity of highlight.
 - Press 'L' to place component on bottom.
 - Disable smart placement: Go to DXP menu --> Preferences, expand "PCB Editor" in the left pane, and select "Interactive Routing". Under the "Dragging" heading, make sure "Component pushing" is set to "Ignore" instead of "Avoid".
 - For complicated PCBs, fan out BGAs, route critical components, 	connect ground and power vias to their planes and then route the tracks.
 - select full trace, select the  part of the trace and press TAB.
 - If you find your self when you can select any thing, a mask is active, click clear on bottom right corner.

# Setup Before routing

__Rules__
- __Clearance__ 
 - Clearance: 0.2 mm  
- __Routing__
   - Min width: 0.3mm, preferred width: 0.3mm, max width: 0.5mm
   - New rule for power net, set width: min:0.4 Preferred:0.4 Max: 4
   - Via diameter: 0.6mm, via hole size: 0.3mm
- __Mask__
   - Solder mask expansion: 0.1mm
- __Manufacturing__
   - Hole to hole clearance: 0.3mm
   - Minimum solder mask silver: 0.3mm
   - Silk to solder-mask clearance: 0.1mm
   - Silk to silk clearance: 0.1mm
- __Placement__
   - Component clearance H&V: 0.2mm 

- Set up rules for ignoring some violations

- Set default Via DXP>Prefs>PCB Editor> Defaults> Via, hole: 0.3mm, diameter: 0.6mm. Force tenting on top and bottom

- __Info from fab__: Minimum clearance, min track width, min via

__Stack up__

- Setup layer stack up in layer manger. Right-click>options>Layer Stack Manager.
- Change layer names to L1 and L2, etc.
- Set thickness of dielectric i.e. PCB thickness, normally 1.6mm 

__Set Layer Views__
- Set for only top layer.
- Set for only bottom layer.
- Set for top and bottom layer.

__Set net colours__
 - Select net in PCB panel, select pad with net>right-click>Change net color. right-click again>Display Override> selected on.
 - Gnd: Blue(236)
 - 5V: Orange(4)
 - 3V3: pink(1)
 - Press F5 to toggle net colours.

 # Routing

- Use interactive routing, press tab to change track parameters on the fly. 
- Shift+R while routing to change modes. Configure modes in DXP>Prefs>PCB Editor>Interactive routing. Disable via pushing.

- After connecting all nets, create power planes, make power tracks wider. Make it look nice.