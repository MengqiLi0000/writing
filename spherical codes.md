## The Geometry of a Crowded Sky

### Spherical codes, broadband constellations, and the point where more satellites stop buying much more coverage

A broadband satellite constellation looks like a communications network, but its first constraint is geometric: **where can points moving on concentric spheres be placed so that every relevant point on Earth sees enough of them, often enough, at a high enough elevation angle?**

That framing puts [Starlink](https://www.starlink.com/), [Eutelsat OneWeb](https://www.eutelsat.com/satellite-network/oneweb-leo-constellation), and [Amazon Leo](https://www.aboutamazon.com/what-we-do/devices-services/amazon-leo) into the same mathematical family as spherical covering, coding theory, lattice design, and stochastic geometry.

The analogy needs one qualification. A broadband constellation is **not a static spherical code**. Its satellites move at roughly 7–8 km/s, the orbital planes are fixed or slowly precessing, Earth rotates underneath, beams steer electronically, and service constraints depend on elevation angle, capacity, gateways, spectrum, weather, and handoff. The actual object is closer to a **time-varying spherical covering subject to orbital dynamics**.

That is more interesting than the static problem.

As of **13 September 2026**, Jonathan McDowell's satellite census counted **11,118 active Starlink satellites** out of **16,790 active payloads in orbit**—about two-thirds of the active satellite population. Eutelsat says its OneWeb Gen-1 network contains **654 spacecraft at 1,200 km**. Amazon says Amazon Leo, formerly Project Kuiper, has now placed **375+ satellites** in orbit toward its licensed first-generation architecture of **3,236 satellites**. [McDowell's live statistics](https://planet4589.org/space/stats/acdec.html) · [Eutelsat responsible-space data](https://www.eutelsat.com/group/sustainability-esg/responsible-space) · [Amazon Leo mission updates](https://www.aboutamazon.com/news/innovation-at-amazon/project-kuiper-satellite-rocket-launch-progress-updates).

Those three systems occupy very different points in the geometry trade space.

| Constellation / shell | Nominal altitude | Inclination | Planes | Satellites / plane | Architecture size |
|---|---:|---:|---:|---:|---:|
| **Starlink Gen-1 shell 1** | 550 km | 53.0° | 72 | 22 | 1,584 |
| **Starlink Gen-1 shell 2** | 540 km | 53.2° | 72 | 22 | 1,584 |
| **Starlink Gen-1 shell 3** | 570 km | 70.0° | 36 | 20 | 720 |
| **Starlink Gen-1 polar shells** | 560 km | 97.6° | 10 total | mixed | 520 |
| **Amazon Leo** | 590 km | 33° | 28 | 28 | 784 |
| **Amazon Leo** | 610 km | 42° | 36 | 36 | 1,296 |
| **Amazon Leo** | 630 km | 51.9° | 34 | 34 | 1,156 |
| **OneWeb Gen-1** | ~1,200 km | 87.9° | 12 | up to ~48 operational + spares | 654 fleet |

Starlink's filed Gen-1 geometry is documented in FCC-derived research as five shells between 540 and 570 km; the first 550 km shell is the familiar **72 planes × 22 satellites** configuration. SpaceX's Gen-2 authorization adds thousands more spacecraft in lower shells, including the 525/530/535 km architecture and newly authorized lower-altitude operations. [FCC Gen-2 order](https://docs.fcc.gov/public/attachments/FCC-22-91A1.pdf) · [2024 lower-shell FCC order](https://docs.fcc.gov/public/attachments/DA-24-1193A1.pdf).

Amazon's first-generation filing is unusually clean geometrically: **98 planes across three concentric shells**—590 km / 33°, 610 km / 42°, and 630 km / 51.9°. The original FCC filing gives **784 + 1,296 + 1,156 = 3,236 spacecraft** and continuous service between roughly **56°N and 56°S** when fully deployed. [Amazon's FCC system description](https://fcc.report/IBFS/SAT-LOA-20190704-00057/1773656.pdf).

OneWeb chooses the opposite end of the altitude trade. Eutelsat's current network uses **600+ satellites in 12 synchronized planes at 1,200 km**, with a near-polar geometry designed for truly global—including polar—coverage. [Eutelsat OneWeb constellation](https://www.eutelsat.com/satellite-network/oneweb-leo-constellation).

<p align="center">
  <img src="assets/constellation_architectures.svg" width="82%" alt="Starlink Amazon Leo OneWeb orbital architecture comparison">
</p>

The different counts are not simply different levels of ambition. They come from different choices about a basic spherical-cap problem.

### One satellite paints a cap on Earth

Take Earth as a sphere of radius

```math
R_\oplus \approx 6371\ \mathrm{km}.
```

A satellite at altitude \(h\) can only serve ground locations for which it appears above some minimum elevation angle \(\varepsilon\). The boundary of that visibility region is a **spherical cap**.

Its central half-angle is

```math
\psi
=
\cos^{-1}\!\left(
\frac{R_\oplus}{R_\oplus+h}\cos\varepsilon
\right)
-
\varepsilon.
```

The corresponding geodesic radius on Earth's surface is

```math
r_g = R_\oplus \psi,
```

and the cap area is

```math
A_{\mathrm{cap}}
=
2\pi R_\oplus^2(1-\cos\psi).
```

<p align="center">
  <img src="assets/spherical_cap_geometry.svg" width="69%" alt="Satellite spherical cap coverage geometry">
</p>

That one equation explains much of the architectural difference between Starlink and OneWeb.

Using the **same 25° minimum elevation mask only as a geometry benchmark**:

| Altitude | Central half-angle \(\psi\) | Ground-radius of footprint | Fraction of Earth's surface in one cap | No-overlap area lower bound |
|---|---:|---:|---:|---:|
| **550 km** | 8.46° | **941 km** | 0.544% | **184 satellites** |
| **610 km** | 9.20° | **1,023 km** | 0.643% | **156 satellites** |
| **1,200 km** | 15.30° | **1,701 km** | 1.772% | **57 satellites** |

The final column is deliberately unrealistic. It is simply \(4\pi R^2/A_{\mathrm{cap}}\), as if spherical caps could tile Earth with no overlap and every sub-satellite point could be placed arbitrarily. Real constellations require far more satellites because they need continuous moving coverage, multiple visible spacecraft, finite beam capacity, handoff margin, restricted orbital inclinations, gateway access, redundancy, and service at useful elevation angles.

Still, the table makes the first trade obvious: **higher altitude buys a much larger footprint**.

<p align="center">
  <img src="assets/footprint_vs_elevation.svg" width="78%" alt="Satellite footprint radius versus elevation angle">
</p>

The price is paid elsewhere.

At zenith, a ground-satellite-ground path through a 1,200 km OneWeb spacecraft has about **2,400 km** of free-space propagation, versus **1,100 km** for a 550 km Starlink-class orbit. Pure geometric light time is therefore roughly **8.0 ms versus 3.7 ms one-way** before routing, processing, terrestrial backhaul, inter-satellite links, queues, or protocol overhead.

At the same radio frequency, the altitude ratio alone also adds approximately

```math
20\log_{10}\!\left(\frac{1200}{550}\right)
\approx
6.8\ \mathrm{dB}
```

of free-space path loss at zenith.

So the first constellation trade is already three-dimensional:

> **higher altitude → fewer satellites for geometric coverage, but longer propagation, more path loss, and a larger physical region swept by each spacecraft.**

OneWeb takes the higher-altitude / larger-cap approach. Starlink uses a much denser set of lower shells. Amazon Leo sits between them.

### The orbit planes create a lattice

Coverage is not determined only by altitude. The satellites have to be placed in orbital planes.

A classical Walker-style constellation is described by three integers—total satellites \(T\), number of planes \(P\), and a phasing parameter \(F\)—plus inclination \(i\). Within an idealized shell,

```math
\Delta\Omega
=
\frac{360^\circ}{P}
```

sets the separation between orbital planes in right ascension of ascending node, while

```math
\Delta u
=
\frac{360^\circ}{S}
```

sets in-plane spacing for \(S=T/P\) satellites per plane.

If \((\Omega,u)\) are treated as angular coordinates, the constellation looks less like points on a sphere and more like a **lattice on a torus**.

<p align="center">
  <img src="assets/walker_lattice.svg" width="79%" alt="Walker constellation lattice">
</p>

Starlink's first 550 km shell is a good concrete example: **72 planes × 22 satellites = 1,584 spacecraft**, inclined at **53°**. A purely in-plane angular spacing is therefore about

```math
\frac{360^\circ}{22}
\approx
16.36^\circ,
```

while adjacent planes are separated in RAAN by

```math
\frac{360^\circ}{72}
=
5^\circ.
```

The lattice moves continuously through Earth-fixed longitude as the satellites orbit and Earth rotates underneath.

Amazon Leo's three shells use a different strategy. Its 590 km layer has **28 planes × 28 satellites**, the 610 km layer **36 × 36**, and the 630 km layer **34 × 34**. The inclinations—33°, 42°, and 51.9°—layer coverage across different latitude bands. The [original Amazon FCC technical appendix](https://fcc.report/IBFS/SAT-LOA-20190704-00057/1773885.pdf) even specifies the deployment order: the first 578 satellites populate half of the 630 km / 51.9° shell, initially serving latitude bands around **39–56° north and south**, then later phases fill progressively toward the equator.

That is a geometric rollout plan, not merely a launch schedule.

### Inclination quietly determines where satellite density accumulates

An orbital inclination \(i\) limits the sub-satellite point to latitudes between \(-i\) and \(+i\) for a prograde orbit below 90°.

The distribution is not uniform inside that band.

If the orbital argument is sampled uniformly, the latitude residence density has the form

```math
p(\phi)
\propto
\frac{\cos\phi}
{\sqrt{\sin^2 i-\sin^2\phi}}.
```

The spacecraft spends relatively more angular time near the turning latitudes of its ground track.

<p align="center">
  <img src="assets/latitude_density.svg" width="80%" alt="Latitude residence density by orbital inclination">
</p>

That makes the shell inclination an economic design variable.

A 33° shell naturally concentrates capacity around lower and mid-latitudes. A 51.9–53° shell reaches much farther north and south. OneWeb's **87.9°** near-polar geometry runs almost pole to pole and is one reason Eutelsat can market coverage in polar aviation, maritime, defense, and Arctic use cases. Eutelsat's 2026 Arctic Winter Games case study explicitly points to the **12 near-polar planes** as the architecture enabling continuous visibility in regions where lower-inclination systems are less naturally dense. [Eutelsat Arctic case study](https://www.eutelsat.com/mediacentre/case-study/satellite-based-live-coverage-arctic-winter-games-2026).

This is also why “number of satellites” is a poor standalone metric. Two constellations with the same \(N\) can produce very different coverage if their inclination sets differ.

### The spherical-code language is useful—but covering is the right problem

A **spherical code** traditionally asks how to place \(N\) points on a sphere to maximize the minimum angular separation between them. That is a packing problem:

```math
\max_{\{x_i\}}
\;
\min_{i\neq j}
d_{\mathbb S^2}(x_i,x_j).
```

Broadband coverage is closer to the dual problem: minimize the largest angular distance from any required ground point to its nearest usable satellite footprint.

That is a **spherical covering problem**.

If \(x_i\) are instantaneous sub-satellite points and \(y\) is a ground point, a simple covering radius is

```math
\rho
=
\max_{y\in\mathcal R}
\min_i
d_{\mathbb S^2}(y,x_i),
```

where \(\mathcal R\) is the service region.

The constellation wants \(\rho\) small enough that every user has a satellite above the required elevation mask.

But broadband systems actually need something stricter than one-cover. They need **k-cover**: enough satellites simultaneously visible for handoff, load balancing, diversity, and resilience.

The relevant event becomes

```math
N_{\mathrm{visible}}(y,t)\ge k
```

for nearly every service location \(y\) and time \(t\).

This is why a simple cap-area calculation understates constellation size so dramatically.

### Why adding 20% more satellites does not buy 20% more coverage

Once coverage caps overlap, returns diminish.

A useful benchmark comes from stochastic geometry. Imagine—unrealistically but instructively—that cap centers were independently and uniformly scattered over a sphere, and each satellite covered fraction \(f\) of the surface.

The expected one-cover fraction is approximately

```math
C(N)
=
1-(1-f)^N
\approx
1-e^{-Nf}.
```

<p align="center">
  <img src="assets/coverage_diminishing_returns.svg" width="79%" alt="Spherical cap coverage diminishing returns">
</p>

This curve is **not a prediction for Starlink, OneWeb, or Amazon Leo**. Real constellations are deterministic, inclination-constrained, time-dependent, and carefully phased. The curve is useful because it isolates a universal effect: overlap.

At small \(N\), new caps find a lot of uncovered surface.

At large \(N\), most new area overlaps something already covered.

There is no true inflection point in this simple exponential—the curve is concave from the start—but there is a practical knee around

```math
Nf\sim1,
```

where random coverage reaches about **63%**.

To reach approximately 95% in this benchmark requires

```math
Nf\approx3,
```

and 99% requires roughly

```math
Nf\approx4.6.
```

That is a nice way to quantify the cost of overlap.

The “20% more satellites” question becomes particularly clean. If a random-cap system starts at coverage \(C\), increasing \(N\) by 20% gives

```math
C'
=
1-(1-C)^{1.2}.
```

The gain depends strongly on where you start.

<p align="center">
  <img src="assets/twenty_percent_marginal_coverage.svg" width="75%" alt="Marginal coverage from 20 percent more satellites">
</p>

| Starting coverage | Coverage after +20% satellites | Gain |
|---:|---:|---:|
| 50% | 56.47% | **+6.47 pp** |
| 80% | 85.50% | **+5.50 pp** |
| 90% | 93.69% | **+3.69 pp** |
| 95% | 97.25% | **+2.25 pp** |
| 99% | 99.60% | **+0.60 pp** |

That is the first important economic result:

> **Near full geometric coverage, another satellite is increasingly a capacity/redundancy purchase rather than a new-area purchase.**

That distinction matters for interpreting today's megaconstellations. Starlink did not need 11,000 satellites merely to make a geometric line-of-sight map turn green. Most of the incremental fleet is buying **capacity, spatial reuse, lower elevation angles, denser handoff, direct-to-cell service, redundancy, and new orbital layers**.

The word “coverage” hides all of those.

### k-coverage is where network engineering enters the geometry

Suppose the number of visible satellites over a point is approximately Poisson with mean \(\lambda\). Then the probability of having at least \(k\) visible satellites is

```math
P(K\ge k)
=
1-
e^{-\lambda}
\sum_{j=0}^{k-1}
\frac{\lambda^j}{j!}.
```

For one-cover, \(\lambda\approx3\) already gives about 95% availability in the random model.

For three-cover, the same \(\lambda=3\) gives only about 58%.

That gap explains why operational constellations are much denser than simple “one satellite visible” geometry suggests. A broadband terminal may want multiple candidates so it can switch beams without waiting for a specific spacecraft, maintain capacity through outages, avoid an obstructed look angle, or hand traffic among satellites as geometry changes every few seconds.

Capacity makes the problem harder again.

A satellite footprint may cover millions of square kilometers geometrically, but it cannot necessarily serve every user inside that footprint at full throughput simultaneously. Phased-array spot beams partition the spherical cap into smaller cells, spectrum is reused across spatially separated beams, and the constellation needs enough satellites overhead to provide **bits per second**, not merely visibility.

So the real optimization has at least three layers:

```math
\text{visibility}
\;\rightarrow\;
\text{k-visibility / handoff}
\;\rightarrow\;
\text{capacity density}.
```

A coverage map is only the first one.

### OneWeb demonstrates the altitude-for-count trade directly

OneWeb's Gen-1 system is almost the cleanest counterexample to the idea that global LEO broadband requires thousands of satellites.

Eutelsat says the operational network has **600+ satellites in 12 synchronized planes at 1,200 km**. Its responsible-space page specifies **654 satellites** in the Gen-1 constellation. [OneWeb constellation](https://www.eutelsat.com/satellite-network/oneweb-leo-constellation) · [Responsible Space](https://www.eutelsat.com/group/sustainability-esg/responsible-space).

The higher altitude means each satellite sees much more Earth. At a common 25° elevation benchmark, the cap area at 1,200 km is more than **3.2×** the cap area at 550 km.

But OneWeb pays for that larger cap with:

- longer propagation distance,
- higher free-space path loss,
- larger physical cells at a given beam angle,
- and an orbital lifetime / debris environment very different from Starlink's much lower shells.

The orbit period is also longer. Using a simple circular-orbit model:

| Altitude | Orbital period | Circular speed |
|---|---:|---:|
| 550 km | **95.5 min** | **7.59 km/s** |
| 610 km | **96.7 min** | **7.56 km/s** |
| 1,200 km | **109.3 min** | **7.26 km/s** |

At 1,200 km, the satellite moves more slowly angularly around Earth and sees a broader surface region. Starlink instead uses density and lower altitude to buy lower slant range and much larger aggregate capacity.

Neither geometry dominates universally.

### Amazon Leo is explicitly layering latitude bands

Amazon's architecture is especially interesting because the three shell inclinations are paired with three different altitudes.

Its licensed Gen-1 design is:

```math
(590\ \mathrm{km},\,33^\circ,\,28\times28),
```

```math
(610\ \mathrm{km},\,42^\circ,\,36\times36),
```

and

```math
(630\ \mathrm{km},\,51.9^\circ,\,34\times34).
```

Amazon's filing says the full 3,236-satellite network is designed for continuous service approximately between **56°N and 56°S**. The initial deployment sequence starts with **578 satellites** in half of the 630 km / 51.9° shell, then adds the 42° layer, completes 51.9°, fills the 33° shell, and finally completes 42°. [FCC filing and deployment sequence](https://fcc.report/IBFS/SAT-LOA-20190704-00057/1773885.pdf).

That ordering is geometrically sensible. A higher-inclination shell creates service in higher-population latitude bands while the network is sparse; lower-inclination shells later add density toward the equator.

Amazon has now moved well beyond the two Protoflight spacecraft launched in 2023. The company renamed Project Kuiper **Amazon Leo on 13 November 2025**, began full-scale deployment in April 2025, and its current mission tracker says it has launched **375+ satellites over 14 missions**. [Rename announcement](https://www.aboutamazon.com/news/amazon-leo/project-kuiper-becomes-amazon-leo) · [live deployment updates](https://www.aboutamazon.com/news/innovation-at-amazon/project-kuiper-satellite-rocket-launch-progress-updates).

In June 2026 Amazon said the upcoming Ariane 6 mission would carry **36 satellites**, while its Kirkland production operation had hundreds more flight-ready. Earlier in March it said the factory was capable of up to **30 satellites per week** and planned **20+ missions** in its second year of deployment. [June 2026 launch update](https://www.aboutamazon.com/news/amazon-leo/amazon-leo-rocket-satellite-update) · [March 2026 cadence update](https://www.aboutamazon.com/news/amazon-leo/amazon-leo-plans-double-launch-rate-20-missions).

The geometry is turning directly into manufacturing cadence.

### Then the problem flips: more points improve coverage but worsen traffic geometry

Coverage is a covering problem.

Collision avoidance is closer to a moving packing problem with uncertainty.

The simplest warning sign is combinatorial. If every object had to be screened against every other object, the number of unique pairs would be

```math
M(N)
=
\binom{N}{2}
=
\frac{N(N-1)}{2}.
```

<p align="center">
  <img src="assets/pairwise_scaling.svg" width="78%" alt="Pairwise conjunction screening scaling">
</p>

A 20% increase in object count does **not** create 20% more possible pairs.

For large \(N\),

```math
\frac{M(1.2N)}{M(N)}
\approx
1.2^2
=
1.44.
```

So **+20% satellites → roughly +44% candidate pairs** before orbital geometry, altitude separation, screening volumes, and temporal filtering remove most of them.

That is the second major result:

> **Coverage benefit becomes sublinear while traffic-management complexity can become superlinear.**

The exact number of operational conjunctions does not scale as \(N^2\), because satellites occupy separated shells, many orbital planes never approach closely, objects are filtered by space and time, and station-keeping is structured. But the pair-count arithmetic explains why traffic management becomes a first-class systems problem once constellations reach thousands of spacecraft.

### Starlink's current maneuver rate shows this is no longer theoretical

SpaceX's FCC reporting provides an unusually large real-world dataset.

For the six months from **June through November 2025**, SpaceX reported **148,696 collision-risk mitigation maneuvers**. The following six-month period brought the annual June-2025-to-May-2026 total to more than **355,000 maneuvers** according to reporting based on SpaceX's FCC submissions. [Published summary of the June–November filing](https://techaptitude.substack.com/p/satellite-collision-avoidance-technology) · [2026 annual-total coverage](https://www.space.com/space-exploration/satellites/every-spacex-starlink-satellite-has-to-dodge-a-collision-almost-weekly-and-experts-fear-the-worst).

SpaceX has also progressively lowered its maneuver threshold. The FCC's Gen-2 record documents an earlier **\(10^{-5}\)** trigger; the 2024 lower-shell order says SpaceX had moved to **\(10^{-6}\)**. SpaceX's later semiannual reporting used an even more conservative **\(3\times10^{-7}\)** threshold. These thresholds matter when comparing maneuver counts: more sensitive policy produces more maneuvers even if the physical environment were unchanged. [FCC 22-91](https://docs.fcc.gov/public/attachments/FCC-22-91A1_Rcd.pdf) · [FCC DA 24-1193](https://docs.fcc.gov/public/attachments/DA-24-1193A1.pdf).

The number of maneuvers therefore is not itself a collision-rate metric.

It is a combination of **orbital density, tracking uncertainty, conjunction geometry, operator threshold, miss-distance criteria, and maneuver policy**.

### Collision probability is a geometry-of-uncertainty problem

Two orbit predictions do not give two exact curves. They give estimated states with covariance.

At the predicted time of closest approach, analysts transform the relative position and uncertainty into an **encounter plane** approximately perpendicular to relative velocity. The combined positional covariance becomes an ellipse; the two spacecraft sizes become a combined **hard-body region**.

The collision probability is the probability mass of the position-error distribution that falls inside that hard-body region.

<p align="center">
  <img src="assets/collision_probability_geometry.svg" width="72%" alt="Satellite collision probability covariance geometry">
</p>

NASA describes the standard probability of collision \(P_c\) exactly this way: the miss distance by itself is insufficient because predicted trajectories have uncertainty. The most widely used methods integrate the relative-position probability distribution over the combined object size. [NASA CARA risk assessment](https://www.nasa.gov/cara/step-2-close-approach-risk-assessment/).

In compact form,

```math
P_c
=
\iint_{\mathcal H}
f_{\Delta \mathbf r}(\mathbf z)\,d\mathbf z,
```

where \(\mathcal H\) is the hard-body region in the encounter plane.

This produces a famous counterintuitive effect: **a smaller covariance is not always safer**. If the nominal miss vector lies just outside the hard-body radius, tightening the covariance can initially push more probability density into the dangerous region before it eventually becomes sufficiently precise to establish a safe miss. NASA's CARA publications call related cases “dilution-region” events and devote substantial work to covariance realism and \(P_c\) uncertainty. [NASA CARA publications](https://www.nasa.gov/cara/cara-publications/).

Collision risk is therefore not just “distance between two satellites.”

It is **distance + object size + covariance + relative geometry + time evolution**.

### Who is actually doing the calculation?

For U.S. civil missions, a large part of the machinery is surprisingly explicit.

[NASA CARA](https://www.nasa.gov/cara/) says conjunction screening for protected NASA assets is driven by the **U.S. Space Force 18th Space Defense Squadron**, which screens trajectories against the high-accuracy space catalog **three times per day for LEO spacecraft**. NASA then performs risk analysis and works with missions on mitigation. Its public workflow is:

1. **Conjunction Assessment** — find close approaches.
2. **Risk Assessment** — evaluate \(P_c\), covariance, consequence, and event evolution.
3. **Collision Avoidance** — plan and execute mitigation if warranted.

NASA says \(P_c>10^{-7}\) merits operational attention and **\(P_c>10^{-4}\)** requires mitigation for its protected assets. [NASA Step 2](https://www.nasa.gov/cara/step-2-close-approach-risk-assessment/).

NASA also publishes much of the math. The [CARA Analysis Tools](https://github.com/nasa/CARA_Analysis_Tools) include open implementations for:

- classical 2-D probability of collision,
- 3-D \(P_c\),
- Monte Carlo \(P_c\),
- collision consequence,
- covariance realism,
- and maximum-\(P_c\) analysis when covariance information is incomplete.

Commercial operators also run their own systems. [LeoLabs](https://leolabs.space/conjunction-alerts/) says its radar network tracks **22,000 satellites, rocket bodies, and hazardous debris fragments**, continuously screens conjunctions, and can issue sequential Conjunction Data Messages in under five minutes. Eutelsat says its OneWeb ground system combines real-time inputs from the U.S. Space Force and LeoLabs; its Gen-1 spacecraft are spaced with passive safety measures and actively managed for collision avoidance. [Eutelsat Responsible Space](https://www.eutelsat.com/group/sustainability-esg/responsible-space).

Amazon's FCC debris authorization similarly requires semiannual reporting of collision-avoidance maneuvers and outages. Its first-generation shells sit at only 590–630 km, and Amazon says satellites normally remain within **9 km of assigned altitude**, partly to reduce overlap with other spacecraft. [Amazon space-safety architecture](https://www.aboutamazon.com/news/innovation-at-amazon/amazon-project-kuiper-space-safety) · [FCC debris order](https://docs.fcc.gov/public/attachments/DA-23-114A1.pdf).

This is not an informal operator courtesy system anymore. It is an algorithmic traffic-management layer running above orbital mechanics.

### Shell separation is itself a traffic-management primitive

Altitude is not merely a communications choice. It partitions traffic.

Starlink's dense operational bands are largely below ~600 km. Amazon Leo occupies 590–630 km. OneWeb sits near 1,200 km. Iridium is near 780 km. Other emerging constellations populate different bands.

The shells reduce conjunction opportunities between satellites that would otherwise repeatedly cross.

But shell separation is imperfect for three reasons.

First, satellites have to **raise orbit after launch and lower orbit for disposal**, so they transit through other altitude bands.

Second, eccentricity and station-keeping tolerances make “550 km” a band rather than a mathematical sphere.

Third, high-inclination orbital planes cross lower-inclination systems in three dimensions even when mean altitudes are separated.

SpaceX's lower-shell FCC authorization explicitly discusses this problem. The Commission allowed lower operational shells and noted the value of altitude flexibility for collision-risk management, while conditioning operations around crewed stations on coordination with NASA. [FCC DA 24-1193](https://docs.fcc.gov/public/attachments/DA-24-1193A1.pdf).

The orbit shell itself is therefore part of the safety architecture.

### A constellation is also a dynamic graph

The geometry does not stop at Earth coverage.

Modern broadband constellations increasingly route traffic through **optical inter-satellite links**, which turn the satellites into nodes of a moving graph.

Amazon's Protoflight satellites demonstrated **100 Gbps optical links over nearly 1,000 km**. [Amazon Protoflight update](https://www.aboutamazon.com/news/innovation-at-amazon/amazon-project-kuiper-latest-updates).

Starlink uses optical links extensively in current-generation satellites. OneWeb's Gen-1 network is more gateway-dependent, while future architectures are adding more onboard processing and flexible payload capabilities.

Now constellation optimization has two simultaneous graph problems:

- Earth-to-space edges: which users can see which satellites?
- space-to-space edges: which satellites can see and route to one another?

At a given time \(t\), the network can be written

```math
G(t)=(V,E_{\mathrm{ground}}(t)\cup E_{\mathrm{ISL}}(t)).
```

The edges appear and disappear as geometry changes.

A constellation that gives perfect ground coverage can still have a poor network topology if gateways or inter-satellite paths are badly placed.

This is one reason altitude, inclination, plane count, phasing, gateways, and laser-link range have to be optimized jointly.

### The deeper optimization is no longer “minimum satellites”

The textbook question—

> How many equal spherical caps cover Earth?

—is only the first line of the actual objective function.

A commercial constellation is closer to:

```math
\min_{\mathcal C}
\quad
C_{\mathrm{spacecraft}}
+
C_{\mathrm{launch}}
+
C_{\mathrm{ground}}
+
C_{\mathrm{operations}}
+
C_{\mathrm{collision\ risk}}
```

subject to constraints on:

```math
\text{coverage probability},
\quad
\text{k-visible satellites},
\quad
\text{capacity density},
\quad
\text{latency},
\quad
\text{elevation angle},
\quad
\text{spectrum interference},
\quad
\text{handoff rate},
\quad
\text{orbital debris risk}.
```

That is why Starlink, OneWeb, and Amazon Leo look so different while solving nominally the same problem.

**Starlink** spends satellite count to buy lower altitude, dense capacity, lower geometric latency, direct-to-cell expansion, and many overlapping service opportunities.

**OneWeb** uses a much higher, near-polar shell to obtain global and polar reach with hundreds rather than many thousands of satellites, accepting a larger link distance.

**Amazon Leo** uses three intermediate shells and inclinations to layer capacity over the populated latitude band, scaling toward 3,236 Gen-1 spacecraft while its 2026 deployment accelerates.

No single one is the “optimal spherical code.” Their cost functions are different.

### The most interesting asymmetry is the one between coverage and traffic

The geometry gives a surprisingly sharp way to summarize the next decade of LEO.

For coverage, overlap creates diminishing returns:

```math
\frac{dC}{dN}\downarrow
\quad\text{as }N\uparrow.
```

For naive pairwise traffic screening:

```math
M(N)\sim\frac{N^2}{2}.
```

So as the constellation grows,

```math
\text{marginal new area}
\downarrow,
```

while

```math
\text{potential pair interactions}
\uparrow\uparrow.
```

This does **not** mean LEO is approaching a simple mathematical carrying capacity; orbital dynamics, shell separation, autonomous maneuvering, more accurate tracking, better ephemeris sharing, and traffic rules all change the effective capacity of the environment.

It does mean that the optimization target changes as networks mature.

The first few hundred satellites are primarily about **making coverage exist**.

The next few thousand are increasingly about **making coverage dense, resilient, and high-capacity**.

At that scale, each additional spacecraft adds less new geography and more interaction with the rest of the orbital system.

The geometry that makes global broadband possible is becoming the same geometry that makes traffic management unavoidable.

> **LEO broadband begins as a spherical covering problem. At megaconstellation scale it becomes a coupled covering-and-avoidance problem: more points improve the communications lattice, while simultaneously making the orbital lattice harder to keep collision-free.**

### Technical reading and live data

**Constellation architecture**
- [FCC — SpaceX Gen-2 authorization, FCC 22-91](https://docs.fcc.gov/public/attachments/FCC-22-91A1.pdf)
- [FCC — SpaceX lower-shell authorization, DA 24-1193](https://docs.fcc.gov/public/attachments/DA-24-1193A1.pdf)
- [Amazon / FCC — original 3,236-satellite Kuiper architecture](https://fcc.report/IBFS/SAT-LOA-20190704-00057/1773656.pdf)
- [Amazon / FCC — deployment sequence and latitude coverage](https://fcc.report/IBFS/SAT-LOA-20190704-00057/1773885.pdf)
- [Eutelsat — OneWeb LEO constellation](https://www.eutelsat.com/satellite-network/oneweb-leo-constellation)
- [Eutelsat — Responsible Space / 654-satellite Gen-1 fleet](https://www.eutelsat.com/group/sustainability-esg/responsible-space)

**Current deployment**
- [Jonathan McDowell — current Starlink statistics](https://www.planet4589.org/space/con/star/stats.html)
- [Jonathan McDowell — active satellite and debris census](https://planet4589.org/space/stats/acdec.html)
- [Amazon Leo — current mission updates](https://www.aboutamazon.com/news/innovation-at-amazon/project-kuiper-satellite-rocket-launch-progress-updates)
- [Amazon — Project Kuiper renamed Amazon Leo](https://www.aboutamazon.com/news/amazon-leo/project-kuiper-becomes-amazon-leo)
- [Eutelsat — 2026 OneWeb replacement satellite order](https://www.eutelsat.com/media-press/media-centre/news/eutelsat-procures-a-further-oneweb-229-leo-satellites-airbus)

**Space traffic and collision probability**
- [NASA CARA — Conjunction Assessment](https://www.nasa.gov/cara/)
- [NASA CARA — Close Approach Risk Assessment](https://www.nasa.gov/cara/step-2-close-approach-risk-assessment/)
- [NASA CARA — publications and probability-of-collision methods](https://www.nasa.gov/cara/cara-publications/)
- [NASA CARA Analysis Tools — GitHub](https://github.com/nasa/CARA_Analysis_Tools)
- [NASA — CARA public software](https://www.nasa.gov/cara/publicly-available-cara-software/)
- [NASA — Starling / Starlink autonomous traffic-coordination test](https://www.nasa.gov/centers-and-facilities/ames/nasa-starling-and-spacex-starlink-improve-space-traffic-coordination/)
- [ESA — Reentry and collision avoidance](https://www.esa.int/content/view/full/413425)
- [LeoLabs — real-time conjunction alerts](https://leolabs.space/conjunction-alerts/)
