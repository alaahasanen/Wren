# Development
This is a development branch, code published here might have bugs and run inconsistently. The reason for publishing this is so that others might have a starting point in there own development.

# Wren

The language and rules for the Wikihouse structural system for 1-3 storey buildings, initially developed in the UK for European contexts.

![Exploded drawing of axonometric joint](https://github.com/wikihouseproject/Wren/blob/master/Images/Wren_overview.jpg)


## Wren Hardware

Wren components are CNC manufactured using structural-grade timber panel materials (typically, plywood) and can be rapidly assembled to produce a structural chassis, onto which other components such as cladding, windows, doors can be fitted.

#### Wren is in development. For full documentation on how Wren works and how you can contribute to its development, visit the [Wren wiki](https://github.com/wikihouseproject/Wren/wiki)

## Wren Parametrics

This version of the Wren structural language has been developed in Grasshopper, the parametric scripting plugin for Rhino 3D. This computational design platform is widely used in the design and construction industries, and is ideally suited to digital manufacturing.

Other formats of the Wren system are currently being developed, but currently this version in Grasshopper format represents the latest thinking and workflow for the structural technology.

It should be taken as a Work in Progress and follows ‘a build something that works first’ approach. There are still several known areas where efficiency can be improved. There are also many ways the script can be extended to make use of Grasshopper’s expansive suite of tools include new features like structural analysis, nesting, GIS data, and solar/environmental tracking. We gladly welcome contributions from fellow computational designers to fork and develop!


### Licence

The repository Grasshopper file WikiHouse_WREN_(v4.3) has been developed by Architecture 00.
Since then this file has been heavily modified by Povl Filip Sonne-Frederiksen and now is in version 4.5.

It is licensed under Mozilla Public License (MPL) version 2.0. For full legal terms of this license visit: https://www.mozilla.org/en-US/MPL/2.0/

### Plugins

This script makes use of the excellent developers toolbox of Grasshopper plugins, which makes this all possible. You will need to download and install the latest versions of these plugins from Food4Rhino.com before opening and running this script file.

The plugins used are:

- [Elefront](http://www.food4rhino.com/app/elefront) - for automated Grasshopper-to-Rhino flow
- [Human](http://www.food4rhino.com/app/human) - for automated Grasshopper-to-Rhino flow
- [FabTools](https://www.food4rhino.com/app/fabtools)- for handling labeling and embedding object attributes.

### Known issues / limits

- **D-Joint splitting of the frame** - there is currently a very basic version of the logic but this probably needs to be custom scripted. The basic rules are no section should be larger than the sheet material (nominally 1220 x 2440mm) and D-joints are never closer than two grips to any corner/junction
- **Integration with Google Sheets** - ~~While you can ‘drive’ the Wren script using the parameter sliders, the best way makes use of the Leafcutter plugin, which connects the script with a google spreadsheet for the input and output of project data. This is particularly handy when setting out the window and door sizes and locations.~~
 - Since its first publishing support for Google sheets has ended. Therefore there currently is no way to store all the parameters. for a building.
Ideal in further iterations of the script it should be optimized and adapted to generate the whole building in one run instead of section by section allowing for all the parameters to be set at the start.

- **Number of roof points** - Here be bugs, it may not work for multiple roof points and may also break the frame/sheathing geometry. Use with care.
- **Tolerance** - While tolerances can be added to slots in the 3D model, a much better/safer approach is to add tolerance offsets to the final nested cutting files, and keep the 3D geometry at 0mm tolerance.
 - This has since been reworked. Tolerance should now be applied correctly for most components.

- **Data Tree structures** - These can be streamlined much further within the Sheathing and Spacer component clusters to improve the file size/solution speed
- Custom scripts - custom C# / Python scripts can and should be added to replace large sections of the script to improve the flow and speed up processing
- **End-walls (in development)** - The gable end walls use the Wikihouse Weaver system (cassette-based) and still more development needed on an automated workflow here, specifically with how the front and rear facades are divided up around window openings. The parametric script for Weaver is not yet included in this initial release.
 - A first draft of a scripted developed by Povl Filip Sonne-Frederiksen has since been provided. As of now it does not follow the Weaver system exactly, but while programming there have been taken considerations to allowed the script to be easily adapted.

- **Notes/comments** -  There’s a definite lack of these in the clusters and subclusters. More detail and comments will be added soon, my apologies! If you have particularly questions get in touch via email or raise an issue here.
 - This is still an issue but an effort has been made to structure and organize large sections of the code.


### Comments by Povl Filip Sonne-Frederiksen
If I would start from scratch I would probably split the logic of the script in to six sections. And then moving the data between them largely using dictionaries to keep the overall structure easily readable.

  **Section**
 1. The first sections is for gathering __all__ parameters that concern the building. This can be split up in to different block pertaining to the geometry of the building and key parameters for fabrication. The reason for keeping it as modular as possible is, that later any platform such as google sheets can be attached to feed the script with data. While ensuring that there are no hard coded value present in other parts of the code ensures that the script behaves as expected if somebody unfamiliar with the project should be using it.
 2. Next a simple line based model of the  building is generated where all reference points are generated and elements are properly sorted and formatted for later use. (in the current state data is often being transformed and resorted to ensure it is in the right format for the following use, this seems to waste computational power)
 3. A third section concerns itself with the generation of the geometry for all slots and tabs. This can very well be further subdivided by component.
 4. The fourth part brings the section two and three together by positioning all tabs and slots in relation to the reference points computed in section 2 and joins them up to form surfaces. This can similarly as section 3 be split up by component.
 5. A 3D model is created separately in section 5 and should be able to easily be turned of to save computation resources. In my opinion a 3 dimensional model consisting of single sheets as should be the result of the previous step is enough to determine the shape and desired appearance.
 6. The sixth and final section takes the output of section 4, labels and prepares it for export by orienting the geometry flat in the work space and arraying it by element.

    **For a simplified version please see the file (Inner and Endwall Test.gh)**  

#### Curent state
- The python components through out the script function as dictionaries to pack and moved data around in a more compact way. For some reasons some don't updated the data perfectly for that timers have been attached to the components that need updating. Those timers can then be run once to force that update. Ideally this issue is addressed in the python component itself and a permanent version of it if made.
- Windows and openings have been briefly tested but a good input method for their location is currently missing therefore this option is not really working.

## Wren Hardware R&D Contributions

**Architecture 00** (www.architecture00.net)
- [Alastair Parvin](https://twitter.com/AlastairParvin)
- [David Saxby](https://twitter.com/davidsx00)
- [Ryan McLoughlin](https://twitter.com/ryanjamesmac)
- [Clayton Prest](https://twitter.com/ClaytonPrest)
- [Nick Ierodiaconou](https://twitter.com/nick_diaconou)
- [Joni Steiner](https://twitter.com/jonisteiner)

**Momentum Engineering** (www.momentumengineering.com)
- Ben Whitfield
- Steve Fisher
- Rosie Stevenson

**Space Craft Systems** (www.spacecraft.co.nz)
- [Danny Squires](https://twitter.com/ecoarknz)
- [Martin Luff](https://twitter.com/martinluff)

**Arup Associates** (www.arup.com)
- Nina Tabink
- Adrian Campbell


**Individual Contributors**
- [Alex Whitcroft](https://twitter.com/AlexWhitcroft)
- Justyna Swat
- Nico Maes
- Akiko Kobayashi

**ULB Bruxelles**
- Structural engineering student group

## Wren Parametric Contributions

**Architecture 00** (www.architecture00.net)
- [Clayton Prest](https://twitter.com/ClaytonPrest)

**Architype - Team Architects** (http://www.architype-ta.co.nz/)
- [Agneesh Brahmbhatt](https://www.linkedin.com/in/agneesh-brahmbhatt-7557234?authType=NAME_SEARCH&authToken=MdJZ&locale=en_US&trk=tyah&trkInfo=clickedVertical%3Amynetwork%2CclickedEntityId%3A13733489%2CauthType%3ANAME_SEARCH%2Cidx%3A1-1-1%2CtarId%3A1482235340928%2Ctas%3Aag)

**Aahus School of Architecture** (https://aarch.dk/)
- [Povl Filip Sonne-Frederiksen](https://github.com/pfmephisto/)
- Matthias Klith Hardarson

If you believe you are missing from either of these lists of historical contributions, please contact us or fork this document to amend.


# Terms of use

By downloading these files or information you agree to the following terms and conditions.

Information is shared without any kind of warranty or guarantee
All Information is provided ‘as is’. No representations or warranties express or implied are made regarding the Wikihouse Info, its accuracy, completeness, functionality or fitness for a particular use in a particular location.  

You are solely responsible for the use of the information
By using this information you assume full responsibility for any loss resulting from use or inability to use the Wikihouse Info, and forever releases WikiHouse Foundation or other WikiHouse users from any liability for such loss;  including but not limited to loss of profits, goodwill or assets.

You are responsible for meeting local codes and legislation
Users must satisfy themselves regarding the application of statutory requirements, local building regulations, codes, insurance certification or other requirements or recommendations relevant to the location where and materials with which they plan to build. Where required you should always seek the advice of a relevant qualified professional.

You are responsible for using the information in a safe way
 Users are responsible for ensuring that information they use or cause to be used is used in a way which is safe, and is not likely to cause harm during or after manufacturing, construction, use or disassembly.
