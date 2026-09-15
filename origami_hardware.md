## When Geometry Becomes Hardware

### Origami mathematics is moving from foldability proofs to flight hardware

Origami is becoming useful in engineering for a reason that has very little to do with resemblance to paper art: **a fold pattern can encode motion before a controller ever sees the mechanism**.

A conventional deployable structure begins with joints and then solves the coordination problem with motors, sensors, latches, bearings, timing logic, and fault handling. Rigid origami begins one level earlier. It chooses a geometry in which many joints are kinematically coupled, so a large structure can move through a narrow set of admissible configurations.

That idea has already crossed the line from laboratory geometry into real aerospace programs. In **1995**, Japan's **Space Flyer Unit (SFU)** carried a two-dimensional solar-array experiment based on **Miura-ori**. NASA/JPL and Brigham Young University later built a radial origami-inspired solar-array prototype that packed to **2.7 m** and was designed to open to **25 m**. NASA's **Structural Origami Array (SOAR)** program now describes a **200 W to 1 kW+** small-satellite array using a two-dimensional origami packaging scheme. At the same time, JPL's **Starshade** program is working on a **34 m** deployable optical structure with petal-placement errors measured in tenths of a millimetre, while BYU researchers are cycling candidate membrane hinges to **10,000 folds**.

Those projects are not variations on the same product. They expose the same underlying engineering question from different directions:

> **Can geometry remove enough mass, volume, actuation, and control complexity to justify the new problems it creates in thickness, tolerance, fatigue, and deployment reliability?**

The interesting part of origami engineering starts there.

<p align="center">
  <img src="https://d2pn8kiwq2w21t.cloudfront.net/original_images/jpegPIA18666.jpg" width="82%" alt="JPL origami-inspired solar array prototype">
</p>

<p align="center"><sub>NASA/JPL-Caltech prototype. Brian Trease holds an origami-inspired solar-array mechanism developed with BYU. Source: <a href="https://www.jpl.nasa.gov/news/solar-power-origami-style/">JPL — Solar Power, Origami-Style</a>.</sub></p>

### The first engineering gain is dimensional reduction

A deployable panel with many independently rotating joints has a large configuration space. If there are \(m\) unconstrained hinge coordinates, the mechanism may require many independent commands to reach the deployed state.

Rigid origami introduces geometric compatibility conditions between those hinges. In the best case, dozens of physical folds can be driven by a single generalized motion.

A degree-4 vertex already shows the idea. Four creases meet at a point, dividing the sheet into sector angles \(\alpha_1,\alpha_2,\alpha_3,\alpha_4\). For a flat-foldable vertex, **Kawasaki's theorem** requires alternating sectors to sum to \(\pi\); **Maekawa's theorem** constrains the mountain/valley assignment.

```math
\alpha_1+\alpha_3
=
\alpha_2+\alpha_4
=
\pi
```

These are not decorative properties. They remove impossible mechanism designs before a motor, material, or controller is selected.

<p align="center">
  <img src="assets/degree4_vertex.svg" width="68%" alt="Degree-4 rigid origami vertex geometry">
</p>

A useful way to understand the same vertex is as a **spherical linkage**. Put an infinitesimal sphere around the vertex: each crease becomes a great-circle direction and the fold becomes a spherical four-bar mechanism. The physical hinges are still there, but their angles are coupled.

That is why the **Miura fold** is mechanically interesting. JPL's 2014 overview put the advantage plainly: for a Miura pattern, pulling one corner can open the whole sheet, so only one input is needed for deployment. JPL also notes that Miura intended the pattern for solar arrays and that a Miura-based panel was deployed on the **Space Flyer Unit in 1995**. [JPL's history is here](https://www.jpl.nasa.gov/news/solar-power-origami-style/); JAXA also describes the SFU two-dimensional solar-array experiment in its [origami-in-space educational material](https://edu.jaxa.jp/activities/SEEC/material/assets/SEEC27-yo.pdf).

<p align="center">
  <img src="assets/miura_lattice.svg" width="78%" alt="Miura-ori lattice geometry">
</p>

This is the first point at which origami can replace hardware. If geometry enforces the coordination that would otherwise be implemented in software and actuators, the mechanism can trade **control complexity for geometric constraint**.

That trade becomes more valuable as the structure gets larger.

### The second gain is packaging density — and spaceflight makes it expensive

Launch vehicles impose both a mass limit and a volume limit. A spacecraft can be light enough to launch and still be impossible to package.

That is why the JPL/BYU radial array was interesting even though it was only a prototype. The full concept was designed to fold to about **2.7 m in diameter** and open to **25 m**. The tabletop demonstrator was built at **1/20 scale** and expanded to **1.25 m**. [JPL documented the dimensions and folding rationale](https://www.jpl.nasa.gov/news/solar-power-origami-style/).

The diameter ratio alone is about **9.3×**. A simple area scaling would imply an order-of-magnitude larger gain in usable deployed surface, although the real packing ratio depends on panel thickness, inactive area, central structure, harnessing, and the actual folded volume.

This is the right way to think about origami hardware: **linear packaging improvements can create much larger deployed-area gains**.

NASA's current **SOAR** project makes the same idea much more explicit. NASA TechPort describes SOAR as a small-satellite array delivering **200 W to 1 kW+** with:

- a **two-dimensional origami packaging scheme**,
- a compact square stowed footprint,
- deterministic two-dimensional unfolding,
- scaling to longer arrays with little increase in stowed height,
- uniform folding mechanics for simpler electrical harnessing,
- and unusual **insensitivity to photovoltaic-cell thickness**.

The last point is especially important. A packaging architecture that tolerates thicker cells can use longer-life or higher-efficiency photovoltaics without redesigning the entire fold stack. [NASA TechPort's SOAR entry](https://techport.nasa.gov/projects/90262) is one of the clearest examples of origami geometry being described in system-level engineering terms rather than as biomimetic inspiration.

### The commercial benchmark is no longer a rigid panel

Origami-inspired arrays are not competing against 1980s solar wings. They are competing against modern deployables that are already flight-proven.

The most important benchmark is **ROSA — Roll-Out Solar Array**, originally developed by **Deployable Space Systems** and now part of **Redwire**. ROSA is not a Miura tessellation; it uses flexible photovoltaic blankets and composite booms that store strain energy and self-deploy. That distinction is useful because it shows what origami has to beat.

NASA says ROSA eliminates the motor-heavy architecture of conventional large arrays by using the composite booms as both structural elements and deployment actuators. The technology has moved from demonstration into operation: **iROSA** units are installed on the International Space Station, ROSA flew on **DART**, and NASA says the design is being used for **Gateway's Power and Propulsion Element** and commercial satellites. [NASA's ROSA impact story](https://www.nasa.gov/directorates/stmd/impact-story-roll-out-solar-arrays/) is a good baseline for what “deployable hardware” now means.

Each ISS iROSA is roughly **18.2 m × 6 m** and produces **more than 20 kW**. NASA says the new arrays collectively increase station power generation by about **30%**. [NASA's 2023 installation report](https://www.nasa.gov/blogs/spacestation/2023/06/15/nasa-spacewalkers-finish-installing-roll-out-solar-array/) gives the flight dimensions and power numbers.

Redwire, meanwhile, has pushed the same deployable lineage into commercial products. Its [solar-array portfolio](https://redwirespace.com/capabilities/solar-arrays-and-deployable-structures/) now spans ROSA, SmallSat arrays, and deployable booms, and in 2026 the company announced **ELSA — Extensible Low-Profile Solar Array**, a compact foldable product aimed at higher-volume satellite production. [Redwire's ELSA announcement](https://ir.redwirespace.com/news-events/press-releases/detail/218/redwire-announces-new-high-performance-low-mass-solar) is useful because it shows the market moving from one-off deployables toward standardized, production-oriented architectures.

The lesson is not that origami “wins.” It is that **packaging geometry has become a commercial design variable**.

### NASA's own 2025 SmallSat catalog shows how wide the performance spread already is

NASA's 2025 state-of-the-art SmallSat report lists very different array architectures side by side:

| System | Architecture | Specific power | Peak BOL power |
|---|---|---:|---:|
| **Redwire ROSA** | Flexible PV blanket | **100 W/kg** | **1,000 W** |
| **Redwire Aladdin** | Flex-rigid hybrid | **80 W/kg** | **300 W** |
| **MMA Design Next-Gen HaWK** | Deployed rigid PCB | **100 W/kg** | **45–310 W** |
| **Pumpkin DCSA** | Deployed rigid | **38–44 W/kg** | **220–350 W** |
| **Space Dynamics Laboratory modular panel** | Deployed rigid | **84.5 W/kg** | **180 W/panel** |

Source: [NASA Small Spacecraft Systems Virtual Institute, 2025 state-of-the-art report](https://www.nasa.gov/smallsat-institute/sst-soa/power-subsystems/).

These are not apples-to-apples products; panel area, cells, voltage architecture, structural margins, mission environment, and power class differ. But the table makes the engineering objective clear. A new origami architecture does not get credit merely for folding. It has to move a real metric: **W/kg, W/L, deployed aperture, actuator count, repeatability, or mission reliability**.

### Then the paper assumption breaks: real panels have thickness

Classical origami assumes zero-thickness facets. Aerospace hardware does not.

Give the panels even a few millimetres of thickness and the ideal crease axis becomes problematic: material from adjacent facets begins to overlap during rotation. The fold may be mathematically valid and mechanically impossible.

<p align="center">
  <img src="assets/thick_panel_collision.svg" width="90%" alt="Zero thickness and finite thickness hinge comparison">
</p>

This is the core problem addressed by **thick-panel origami**. Engineers use offset hinge axes, bevels, compliant hinges, split creases, material removal, and hybrid origami-kirigami layouts to recover a collision-free path.

A particularly concrete example is the 2025 *Nature Communications* paper **“Thick-panel origami structures forming seamless surfaces”** by **Rui Peng and Gregory Chirikjian**. The paper is valuable because it does not stop at a foldability proof. It converts facets into rigid panels, creases into rotational joints, derives motion-compatibility conditions, removes interference around valley creases, and then fabricates physical prototypes. [Open-access paper](https://www.nature.com/articles/s41467-025-59141-2).

<p align="center">
  <img src="https://media.springernature.com/lw685/springer-static/image/art%3A10.1038%2Fs41467-025-59141-2/MediaObjects/41467_2025_59141_Fig1_HTML.png" width="88%" alt="Nature Communications thick-panel origami structures">
</p>

<p align="center"><sub>Peng & Chirikjian, <i>Nature Communications</i> 16, 3881 (2025). Fully deployed and folded thick-panel structures, including seamless and curved-trajectory variants.</sub></p>

The manufacturing details are unusually revealing. The prototypes were printed in **PLA**, mainly on a **Bambu X1C**, with larger parts made on a **Raise3D Pro3**. Rotational joints were integrated into the panels and connected using **2 mm steel pins**.

That is where the field becomes interesting: the abstract crease has turned into a pin diameter, panel thickness, bevel angle, interference envelope, and assembly process.

The same paper derives a simple interference condition around the modified valley region. The point is less the formula than the design logic: panel thickness \(h\), joint spacing \(d\), extension length \(t\), and wedge angle \(\alpha\) have to be chosen together so the moving panels clear one another.

<p align="center">
  <img src="https://media.springernature.com/lw685/springer-static/image/art%3A10.1038%2Fs41467-025-59141-2/MediaObjects/41467_2025_59141_Fig4_HTML.png" width="88%" alt="Nature thick panel motion interference geometry">
</p>

<p align="center"><sub>The paper's interference geometry. This is the practical thick-panel problem: preserve the desired kinematics while changing the physical panel shape enough to keep the path collision-free.</sub></p>

One version of the design also reduces the top layer from **18 panels to 12** while preserving the same folded and deployed dimensions — a **33% reduction in panel count**. That is the kind of geometric simplification that can propagate into fewer joints, fewer tolerance interfaces, less assembly, and potentially lower failure exposure.

### The field is also moving beyond solar arrays

**Origami Space Development**, a Colorado startup, is applying deployable geometry to **RF and LiDAR apertures** rather than power systems. The company says its satellite architectures target communications, intelligence, digital twins, and space-domain awareness. In 2025 it announced a **NASA Phase II SBIR** to advance a **Folding Origami Inspired LiDAR Aperture**, using arrays of millimetre-thick metalenses as an alternative to massive conventional mirrors and lenses. [Origami Space](https://www.origamispace.com/) | [NASA Phase II announcement](https://www.origamispace.com/news/6h3rswkn39fnhmzc25fx1m2wi84v06).

It was also selected for the **DARPA ERIS Marketplace** with an “Origami Deployable Antenna Technology” concept. [DARPA selection announcement](https://www.origamispace.com/news/darpa-selection).

The company is still early-stage, so these should be treated as development programs rather than deployed commercial heritage. But they show why the problem is broader than solar power: any payload whose useful aperture is much larger than its launch envelope is a candidate.

NASA Langley is pushing the same idea into **load-bearing structures**. Its **Origami-Based Deployable Composite Super-Structures** program combines shape-memory polymer hinges with rigidizable composites for lunar/Mars habitat substructures and payload-transfer systems. NASA's licensing portal says the current carbon-fiber / polymer concept can deploy through heat rather than motors and has demonstrated **at least 600 kg load capacity on Earth** in prototype testing; the technology is listed at **TRL 4**. [NASA TechPort](https://techport.nasa.gov/projects/146566) | [NASA Technology Transfer](https://technology.nasa.gov/patent/LAR-TOPS-372).

That is a different destination for the same mathematics. The solar-array question is “how much area can I deploy?” The habitat question is “how much load-bearing structure can I launch in a small package?”

### Starshade is where deployable geometry becomes metrology

JPL's **Starshade** work shows how demanding the problem becomes when the deployed edge is optical hardware.

The full-scale concept tested at JPL corresponds to a **34 m diameter** starshade. Each petal is about **7 m long**. The petals must unfold around a **20 m central disk** and recover their positions to a fraction of a millimetre. JPL reports that across **20 deployments**, the test structure placed the petals within roughly **0.1 mm** of the correct location each time. [JPL Starshade laboratory summary](https://microdevices.jpl.nasa.gov/capabilities/optical-components/starshade/).

<p align="center">
  <img src="https://d2pn8kiwq2w21t.cloudfront.net/original_images/jpegPIA20907.jpg" width="88%" alt="JPL starshade deployment sequence">
</p>

<p align="center"><sub>NASA/JPL-Caltech/Princeton. Half-scale starshade deployment sequence. The full-scale design represented by this test article is 34 m across. Source: <a href="https://www.jpl.nasa.gov/images/pia20907-starshade-deployment/">JPL Photojournal</a>.</sub></p>

NASA's current technology-gap documentation is even more explicit. For a 34 m class system, it calls for petal deployment within an approximately **1 mm in-plane envelope** and petal-edge shape tolerances near **100 μm**. [NASA Exoplanet Exploration technology progress report](https://assets.science.nasa.gov/content/dam/science/astro/programs/exep/technology/files/Progress_in_Technology_for_Exoplanet_Missions.pdf).

JPL's **Advanced Large Precision Structures Laboratory** describes the test scale another way: a **34 m aperture** that must stow into roughly a **4 m launch cylinder**. The same laboratory tests deployables from CubeSat-scale **50 cm apertures inside 10 × 20 × 30 cm spacecraft** up to Starshade class structures. [JPL ALPS Laboratory](https://www.jpl.nasa.gov/site/research/research-community/laboratories-facilities/advanced-large-precision-structures-alps-laboratory/).

<p align="center">
  <img src="assets/starshade_tolerance.svg" width="70%" alt="Starshade petal tolerance geometry">
</p>

The scale ratio is severe. A 34 m structure with 0.1 mm repeatability is operating across a length-scale ratio of roughly **340,000:1**.

At that point, “deployable” is not enough. The mechanism must be **repeatably deployable**.

### Fold geometry eventually becomes a fatigue problem

For one-shot spacecraft mechanisms, the main reliability question may be a single successful deployment after launch vibration, storage, vacuum, and thermal cycling.

For retractable arrays, robots, morphing structures, and lunar infrastructure, cycle life becomes first-order.

A fold concentrates curvature. Smaller fold radii improve packaging but increase material strain. That means stowed volume and fatigue life can work against each other.

BYU's 2026 study **“Cyclic Testing of Membrane Hinges for Use in Origami-inspired Engineering Design”** is useful because it tests the hinge itself rather than treating the crease as ideal. The researchers evaluated:

- **three polymers**,
- **fiberglass**,
- **three steels**, including stainless-steel mesh,
- all at **0.076 mm thickness**,
- under fully reversed loading with a constrained minimum radius.

The hinges were tested to **10,000 cycles** because the authors expect many deployable origami applications to operate in a relatively low-cycle regime. The polymers and fiberglass exceeded the full 10,000-cycle test without complete failure; the metal samples showed material-dependent damage and failure. [BYU ScholarsArchive](https://scholarsarchive.byu.edu/facpub/9651/).

There is no universal answer to “what happens after 1,000 folds?” Two published systems demonstrate why.

A 2021 **origami continuum robot** by Junius Santoso and Cagdas Onal reported only **3.14% maximum change in axial stiffness after 1,000 cycles**. The same structure was approximately **73× stiffer in torsion** than the silicone soft actuator used for comparison, illustrating how much stiffness can come from geometry rather than bulk material alone. [Soft Robotics paper](https://journals.sagepub.com/doi/10.1089/soro.2020.0026).

A 2026 *Advanced Science* paper on the **Tri-WOB bistable origami structure** reported stiffness falling from **15.26 N/mm to 13.49 N/mm after 1,000 cycles** — an **11.6% reduction**. The authors attributed additional force degradation partly to increasing misalignment between opposing vertices. [Tri-WOB paper](https://advanced.onlinelibrary.wiley.com/doi/10.1002/advs.76898).

<p align="center">
  <img src="assets/fatigue_1000_cycles.svg" width="72%" alt="Published origami stiffness changes after 1000 cycles">
</p>

The chart should not be read as a head-to-head material comparison. The mechanisms and loading modes differ. That is precisely the point: **“origami” is not a material property**. Fold life belongs to a particular geometry-material-hinge system.

### Reliability gets harder as the mechanism gets larger

If a mechanism contains many independently critical folds, component reliability compounds.

For illustration, if each of 40 critical hinges has **99.9%** probability of surviving the mission and failures are independent, system survival is only about **96.1%**.

<p align="center">
  <img src="assets/hinge_reliability.svg" width="72%" alt="System reliability versus critical hinge count">
</p>

This is one reason low-degree-of-freedom architectures are interesting even when they do not save much mass. Reducing the number of independent actuators, latches, or controlled states can remove failure opportunities.

NASA makes the same argument in a different architecture. Its [ROSA impact story](https://www.nasa.gov/directorates/stmd/impact-story-roll-out-solar-arrays/) emphasizes that using strain-energy composite booms instead of a conventional motorized deployment chain reduces the number of components that can jam or fail.

Origami tries to push that logic one level further: **let geometry perform some of the synchronization**.

### There is now a real design space, not a single “best fold”

The commercial question is not whether Miura-ori is superior to ROSA, Starshade, a rigid-panel wing, or a shape-memory composite beam. Those systems optimize different objectives.

A small-satellite power system may value:
- stowed square cross-section,
- harness simplicity,
- W/L,
- and low deployment shock.

A lunar surface array may value:
- retractability,
- dust tolerance,
- vertical deployment,
- and cycle life.

An RF aperture may value:
- surface RMS error,
- deployed stiffness,
- and thermal stability.

A starshade values:
- edge shape,
- repeatability,
- and dimensional stability over tens of metres.

A load-bearing habitat structure values:
- buckling resistance,
- deployed rigidity,
- and structural mass.

The correct abstraction is therefore not “origami versus non-origami.” It is a constrained system-design problem over **packaging, mass, stiffness, degrees of freedom, deployment accuracy, cycle life, and failure probability**.

### The nearby mathematical story: reducing a 2-D problem to 1-D

The 2026 **Strait Guarding** result is worth placing next to this field, with one caveat: it is a computational-geometry result, not an origami result.

Its conceptual relevance is that it uses geometry to reduce dimensionality. Under the paper's weak-visibility conditions, guarding a polygon boundary from a designated base edge is enough to guard the interior, turning a planar coverage problem into an optimization over a line.

Rigid origami makes a mechanically analogous move: many physical hinge coordinates can collapse onto a low-dimensional admissible path.

That shared idea is more important than any literal connection between the two literatures:

> **Good geometry removes decisions from the system.**

In one case it removes search dimensions. In the other it removes mechanical degrees of freedom.

### The engineering timeline is getting shorter

The progression is now visible in actual programs:

| Year | Program / system | What changed |
|---|---|---|
| **1995** | **JAXA Space Flyer Unit** | Miura-based two-dimensional solar-array experiment deployed in orbit |
| **2014** | **JPL + BYU radial array** | 2.7 m stowed / 25 m conceptual deployed diameter; thick-panel packaging becomes explicit |
| **2017** | **ROSA ISS demo** | Roll-out architecture demonstrates autonomous composite-boom deployment in orbit |
| **2021–2023** | **iROSA** | Operational ISS power hardware; >20 kW per array |
| **2025** | **Peng & Chirikjian thick-panel origami** | Seamless thick-panel surfaces, explicit collision geometry, physical 3D-printed joints |
| **2025** | **Origami Space NASA Phase II** | Folding LiDAR aperture moves origami geometry into optical payload architecture |
| **2026** | **NASA SOAR update** | 200 W–1 kW+ origami-packaged SmallSat array documented as completed tech project |
| **2026** | **BYU hinge fatigue study** | Polymer, fiberglass, and steel membrane hinges tested to 10,000 cycles |
| **2026** | **Tri-WOB** | Published 1,000-cycle degradation data for bistable variable-stiffness origami |

The dates do not describe one technology curve; they show a field filling in its missing layers. First came foldability. Then packaging. Then flight deployment. Then thick panels, optical tolerances, fatigue, and manufacturing.

That is exactly what one would expect if origami were turning from a mathematical design language into an engineering platform.

### What still has to be solved

The hard problems are now fairly concrete.

**Thickness accommodation.** Zero-thickness mathematics remains much cleaner than real panel kinematics. Thick-panel methods work, but often add joints, bevels, offsets, or local material removal.

**Tolerance accumulation.** A mathematically one-DOF mechanism can still bind if hinge axes are misaligned or panel dimensions drift. Precision systems such as Starshade push this into sub-millimetre metrology.

**Fatigue.** Ten-thousand-cycle hinge data is encouraging for some polymers and fiberglass, but repeated deployment is still highly material- and geometry-specific.

**Structural performance.** Some recent thick-panel papers explicitly leave load-bearing comparison for future work. A fold pattern that packages beautifully can still be too compliant after deployment.

**Qualification.** Launch vibration, thermal-vacuum cycling, radiation, contamination, dust, and long-duration creep can matter more than room-temperature folding demonstrations.

**Economics.** More intricate geometry is not free. It can reduce launch volume while increasing fabrication, metrology, or qualification cost.

The right economic condition is simple even if the engineering is not:

```math
\text{value of mass + volume + mechanism reduction}
>
\text{design + qualification + reliability penalty}
```

That is the point at which an elegant fold becomes useful hardware.

### The deeper shift

The oldest version of origami asks:

> What three-dimensional shape can this sheet become?

Engineering origami increasingly asks the inverse question:

> What geometry should I encode in the flat or stowed state so that the mechanism can only become the structure I need?

That is a much more powerful formulation.

It turns a crease pattern into a **mechanical program**.

The most convincing evidence is no longer a paper crane or even a clever fold. It is **a 34 m optical structure repeating to 0.1 mm, a 20+ kW array operating on the ISS, a 600 kg load-bearing shape-memory composite prototype, a 2 mm steel-pin thick-panel joint, and a membrane hinge still alive after 10,000 cycles**.

Those are not origami numbers.

They are hardware numbers.

> **Origami becomes deployable engineering when the geometric constraint survives the conversion from ideal creases to real joints — and still creates a better mass, volume, precision, or reliability trade than the conventional mechanism it replaces.**

### Sources and technical reading

- [NASA/JPL — Solar Power, Origami-Style](https://www.jpl.nasa.gov/news/solar-power-origami-style/)
- [JAXA — Applying Origami to Space Technology](https://edu.jaxa.jp/activities/SEEC/material/assets/SEEC27-yo.pdf)
- [NASA TechPort — Structural Origami Array (SOAR)](https://techport.nasa.gov/projects/90262)
- [NASA — Roll-Out Solar Array technology impact](https://www.nasa.gov/directorates/stmd/impact-story-roll-out-solar-arrays/)
- [NASA — ISS iROSA installation, dimensions and power](https://www.nasa.gov/blogs/spacestation/2023/06/15/nasa-spacewalkers-finish-installing-roll-out-solar-array/)
- [Redwire — Solar arrays and deployable structures](https://redwirespace.com/capabilities/solar-arrays-and-deployable-structures/)
- [Redwire — ELSA compact foldable array](https://ir.redwirespace.com/news-events/press-releases/detail/218/redwire-announces-new-high-performance-low-mass-solar)
- [Nature Communications — Thick-panel origami structures forming seamless surfaces](https://www.nature.com/articles/s41467-025-59141-2)
- [Origami Space — deployable RF and LiDAR architectures](https://www.origamispace.com/)
- [Origami Space — NASA Phase II Folding Origami Inspired LiDAR Aperture](https://www.origamispace.com/news/6h3rswkn39fnhmzc25fx1m2wi84v06)
- [NASA TechPort — Origami-Based Deployable Composite Super-Structures](https://techport.nasa.gov/projects/146566)
- [NASA Technology Transfer — Origami-based Deployable Fiber Reinforced Composites](https://technology.nasa.gov/patent/LAR-TOPS-372)
- [JPL — Starshade laboratory](https://microdevices.jpl.nasa.gov/capabilities/optical-components/starshade/)
- [JPL — Advanced Large Precision Structures Laboratory](https://www.jpl.nasa.gov/site/research/research-community/laboratories-facilities/advanced-large-precision-structures-alps-laboratory/)
- [NASA — Starshade technology development](https://science.nasa.gov/astrophysics/programs/exep/technology/starshade/)
- [BYU — Cyclic Testing of Membrane Hinges for Origami-inspired Engineering](https://scholarsarchive.byu.edu/facpub/9651/)
- [Soft Robotics — Origami Continuum Robot](https://journals.sagepub.com/doi/10.1089/soro.2020.0026)
- [Advanced Science — Tri-WOB bistable origami structure](https://advanced.onlinelibrary.wiley.com/doi/10.1002/advs.76898)
- [NASA — 2025 SmallSat power-system state of the art](https://www.nasa.gov/smallsat-institute/sst-soa/power-subsystems/)
