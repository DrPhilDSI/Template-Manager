# Insert into Fixture Framework

## Functionality Overview:

The addin will provide guide people through inserting CAD into a lineage with specific attachments for use in the wider framework documented in this [AU presentation](https://www.autodesk.com/autodesk-university/class/Templates-Configurations-and-Containers-for-Agile-Prototype-Machining-in-Autodesk-Fusion-2024)

The framework is available on [Github](https://github.com/Philip-Mestenhauser/Fusion-Workflow-Template-Framework)

[Documentation](https://github.com/Philip-Mestenhauser/Fusion-Workflow-Template-Framework/blob/main/ClassHandout-MFG3914-Mestenhauser-AU2024.pdf) for manually rigging Fixture assets into the framework

## High level process sequence and intent that could be guided for a user by an addin

This process will guide people to creating Replaceable Fixturing assets.

Bonus points if it works to rig the joint origins onto a vise Configuration

- Step 1: Import CAD data into Lineage

  User opens a CAD file, either internally managed, or File-Open from my Computer.

  Prompt should require the relevant metadata for Product ID, Manufacturer, Web link, and Type of Fixture. Write to attributes for use later and naming /navigating the output design file into directories

  - Needs to support users who have existing CAD assets
    - Best practice to simplify geometry - nudge users to do so, or do it for them
    - Pre-existing CAD needs joint origins removed
    - Disable Design history to clean into dumb components
    - Sorted into minimum Components for motion
    - Create a Component container and move all geometry into it.
    - Enable Design history
    - Simplify geometry with simplify tool to leave a history of simplification
  - Needs to support users importing from manufacturer provided .step
    - Disable Design history
    - Manufacturer provided dumb .step or other file types will need to be sorted into minimum Components for motion
    - Create a Component container and move all geometry into it.
    - Enable Design history
    - Simplify geometry with simplify tool to leave a history of simplification
    - Slider or other relevant motion should be added
    - GtP the base to the origin
  - Position all geometry on the coordinate Origin of the container of Geometry
    - Vises should be positioned above the origin at the zero point
    - Clamping units should be positioned above the Origin at the zero point attachment
    - WCS geometry should be positioned above the Origin
  - Insert Component container with all Geometry + motion joints into the lineage file - GTP the container
  - Guide users to select the relevant mounting points using snap points - disallow the input of the Root origin
  - Save file into relevant data panel location

- Step 2: Assist in Assembly of Fixturing Assemblies.
  Using the data in the Fixturing library an addin could assist in making new fixture assembles. This is fairly easy for a user - they simply need to open the Ancestor Fixture Assembly, and replace any filetype inside with their own.

  - It could be a light assembly environment, where they could add multiple vises each auto-joining onto the correct Zero Point Attachments.
  - Save this design for the user

- Step 3: Using the Fixture Assembly in a Template.

  One challenge is bringin in an additional setup. It could be cool if you could just click a button in Fusion to “Add setup” where it brings in a new Fixture Assembly inside a Component container to keep the Browser organized.
  Then in the MFG workspace, create a new setup, and point the Model to the Model Container, the Stock to the Stock Container, the fixture to the Fixture container inside the new Fixture Assembly, and finally each WCS selection for Z/X/WCS

- Step 4: Managing all your damn templates in the first place.
  IDK but this problem is real.

## Challenges

- That Darn Data panel
  It’s hard to find things in the data panel, and since the Ancestors likely need to live in a folder that has a known URN - we might want to consider making a couple folders that the library assets will be copied into as the Insert into Fixture Framework addin runs

  - Fixturing Library:

    - Ancestors
    - Fixture Assemblies
    - Vises
    - Clamping units
    - WCS

  - Managing a bunch of templates once they exist.
  - The current framework doesn’t have a ‘Model Attach point’ it probably should
