
27/10/2025
***

# <span style="color:rgb(223, 109, 109)">Simulating Single Neuron and Network Acitivity</span>

This session was a **practical lesson and guest lecture**, focused on simulating neuronal dynamics and synaptic mechanisms using computational models.

### Topics covered:

- **Leaky Integrate-and-Fire (LIF) model simulation**
- **Hodgkin–Huxley model simulation**
- **Plastic synapse simulation**
- **Cortical circuit simulations** _(extra)_

All simulations were performed through the **EBRAINS** platform.

![[Pasted image 20251101090821.png]]

## <span style="color:rgb(239, 179, 1)">Simulation Software: NEST Desktop</span>

![[Pasted image 20251101091439.png]]
**NEST Desktop** is a simulator that allows users to create, connect, and record the activity of neurons in a network.  
It is built on **Python**, and although it includes a coding backend, the **graphical user interface (GUI)** makes it very intuitive and accessible for non-programmers.

The tool provides multiple built-in features for:

- Constructing neuronal networks
- Visualizing connections and activity
- Analyzing and interpreting results

This environment bridges **computational neuroscience** and **experimental understanding**, allowing users to explore neuronal dynamics without requiring deep programming experience.

![[Pasted image 20251101091455.png]]

We’ll start by recalling some theoretical aspects.  The **Leaky Integrate-and-Fire (LIF)** model is the simplest neuron model. It’s computationally light but has **low biological plausibility**. All neuron models share this trade-off:

- **Simple models** (like LIF) are easy to implement and simulate large networks (thousands or millions of neurons).
- **More detailed models** (like Hodgkin-Huxley) are more biologically realistic but computationally expensive.
    
The LIF neuron behaves like a simple **RC circuit**.  It integrates incoming current until the **membrane potential** reaches a threshold.  
Once this threshold is crossed, the neuron **fires a spike** and resets.
## <span style="color:rgb(239, 179, 1)">Computational Modeling Tools</span>

Several simulation platforms are available for modeling neural systems at different levels of complexity:

- **NEST** → for point-neuron models and spiking neural networks _(used today)_
- **NEURON** → for multi-compartmental models with detailed biophysics
- **The Virtual Brain (TVB)** → for large-scale brain simulations based on physical and physiological data
- **Arbor** → for morphologically detailed multi-compartmental neuron models
- **Brain Scaffold Builder** → for constructing morphologically detailed networks

All these simulators are part of the **EBRAINS** ecosystem, providing a powerful infrastructure for computational neuroscience

# <span style="color:rgb(223, 109, 109)">From Simple to Complex Models</span>

After exploring the LIF model, the next steps involve:

1. **Synaptic modeling** — introducing synaptic currents and their dynamics.
2. **Plasticity simulations** — studying how synapses adapt and learn.
3. **Cortical circuit simulation** — integrating all components to reproduce network-level activity.
    
If time allows, we’ll reach the cortical simulation; otherwise, it will remain as an exercise to explore individually.


# <span style="color:rgb(223, 109, 109)">Lab Introduction</span>

To start, open **NEST Desktop** from the EBRAINS platform.  
You can simply search **“NEST Desktop”** on Google — the first result should be the official EBRAINS page:

🔗 [https://www.ebrains.eu/tools/nest-desktop](https://www.ebrains.eu/tools/nest-desktop)

![[Pasted image 20251101133239.png]]
## <span style="color:rgb(239, 179, 1)">Creating a New Project</span>

Once inside, you can either open one of the **example projects** (like _Spike Activity_) or create a **new one from scratch**.  
The workspace looks like this 

 **Network elements:**
- **Neurons**
- **Stimulators**
- **Recorders**
    

To start a **new simulation**, click **New Project**, give it a name, and save it immediately.  

![[Pasted image 20251101133426.png]]

 _Tip:_ It’s a good habit to save early — sometimes the browser might refresh or freeze during simulation, and saving ensures you don’t lose progress.

![[Pasted image 20251101134231.png]]

## <span style="color:rgb(239, 179, 1)">Building the LIF Neuron Network</span>

![[Pasted image 20251101134243.png]]
1. **Right-click** on the workspace → a small menu will appear with options to add nodes:
    
    - **S** → Stimulator
    - **N** → Neuron
    - **R** → Recorder
        
2. **Create a neuron node**
    
    - Choose the model: **“Integrate-and-Fire PSC”**  
        (This stands for _post-synaptic current_ and is a simple point-neuron model.)
        
3. **Create a stimulator node**
    
    - Select **“Direct Current Generator”**, which provides a **step current** stimulus (constant input over time).
    - This acts like the external current that charges the neuron’s membrane.
        
4. **Create recorders**
    
    - **Voltmeter** → records the membrane potential (difference between internal and external voltage).
    - **Spike Recorder** → records when a spike occurs (1 = spike, 0 = no spike).

## <span style="color:rgb(239, 179, 1)">Connecting the Components</span>

![[Pasted image 20251101134554.png]]

Now connect the components using the small **circles** (connection ports) on each node:

1. **Stimulator → Neuron**  
    The current is sent from the stimulator to the neuron.
    
2. **Voltmeter → Neuron**  
    The voltmeter measures the neuron’s membrane potential.  
    _(If you connect them in reverse, NEST Desktop will automatically correct the direction.)_
    
3. **Neuron → Spike Recorder**  
    The spike recorder receives the output spikes from the neuron.
    
 At the end, your network should look something like this:

![[Pasted image 20251101134734.png]]

Now...  

### <span style="color:rgb(161, 40, 226)">Controlling the Network (right-hand panel) — quick guide</span>
![[Pasted image 20251101135545.png]]

- **Right panel = control & parameters**  
    Everything you create in the canvas has a panel on the right where you can: change model type, set parameters, and inspect population settings.

![[Pasted image 20251101135600.png]]


- **Python backend**  
    All GUI actions generate a Python script behind the scenes (`nest.create`, `nest.connect`, `nest.simulate`, ...). You don’t need to code now, but the code is available if you want to export or edit it later.

***
***
***
***
***
# <span style="color:rgb(223, 109, 109)">1. Leaky Integrate-and-Fire (LIF) Model Simulation</span>

## <span style="color:rgb(239, 179, 1)">1.1 Exploring the Membrane Potential Response</span>

![[Pasted image 20251101140530.png]]

![[Pasted image 20251101153024.png]]

We start by stimulating a single neuron modeled as a _Leaky Integrate-and-Fire_ (LIF) unit.  
In this model, the neuron behaves like an **RC circuit**:

- The _membrane capacitance_ $C_m$​ stores charge.
    
- The _membrane resistance_ $R_m$​ allows the leakage of current.  
    Together, they define the **membrane time constant** $\tau_m = R_m \times C_m$.
    
### <span style="color:rgb(161, 40, 226)">Setup</span>

- **Stimulus type:** Direct Current (DC generator)
- **Amplitude:** Start with **100 pA**
- **Start time:** 100 ms
- **Stop time:** 500 ms
    
- **Recording:** Voltmeter connected to the neuron
    

This configuration produces a **square current pulse**:  
0 pA → 100 pA (between 100–500 ms) → 0 pA again.

### <span style="color:rgb(161, 40, 226)">Observation</span>
![[Pasted image 20251101140630.png]]

- When the current is **positive**, the membrane potential **depolarizes** gradually (charging phase).    
- It then **stabilizes** near a steady value while the stimulus is on, and finally **decays exponentially** back to rest when the current stops.
- The exponential rise and decay reflect the **RC charging and discharging** behavior of the membrane.
    
If we instead apply a **negative current**, the potential **hyperpolarizes**, moving further away from the firing threshold and never producing a spike.
## <span style="color:rgb(239, 179, 1)">1.2 Increasing Current Amplitude</span>

![[Pasted image 20251101140722.png]]

![[Pasted image 20251101140750.png]]


Try increasing the amplitude from **100 pA → 200 pA → 300 pA**, etc.  
You will notice:

- The **depolarization becomes stronger** (membrane potential reaches higher values).
- Once it crosses the **threshold voltage** (e.g. around –55 mV), the neuron **fires a spike**, (input direct current 380pA).
- After firing, the potential **resets instantly** (to a reset value, e.g. –70 mV), then starts charging again as long as the stimulus remains.
- With higher currents, **spike frequency increases**, until saturation occurs.

![[Pasted image 20251101152735.png]]


## <span style="color:rgb(239, 179, 1)">1.3 Effect of Biophysical Parameters</span>

Let’s explore how the parameters influence the membrane potential trajectory:

| Parameter                                  | Meaning                                  | Effect when Increased                            |
| ------------------------------------------ | ---------------------------------------- | ------------------------------------------------ |
| **Spike threshold (V<sub>th</sub>)**       | Minimum voltage to fire                  | Fewer spikes, requires stronger current to fire  |
| **Membrane time constant (τ<sub>m</sub>)** | How fast the membrane charges/discharges | Slower rise and decay, smoother voltage response |
| **Absolute refractory period**             | Time neuron stays inactive after spike   | Longer pauses between spikes, lower firing rate  |
## <span style="color:rgb(239, 179, 1)">1.4 Exploring Model Parameters and Physiological Meaning<br></span>
Now that we have a functioning LIF neuron simulation, we can start **tuning its parameters** to see how the neuron’s firing behavior changes.  
This is the power of computational modeling — we can reproduce different neuron types or behaviors by adjusting a few key biophysical parameters.

### <span style="color:rgb(161, 40, 226)">1.4.1 Adjusting the Spike Threshold</span>

Different neurons in the brain have **different levels of excitability** — some fire easily, while others require stronger inputs.

Let’s try:

- **Spike threshold = –40 mV**
    
With this higher threshold, the neuron becomes **less excitable**.  
For the same 100 pA input current, **the neuron will not spike**, since the depolarization never reaches the new threshold.

 In general:

- Lower threshold → **more easily excitable** neuron (more spikes)
- Higher threshold → **less excitable** neuron (fewer or no spikes)
    


### <span style="color:rgb(161, 40, 226)">1.4.2 Membrane Time Constant (τₘ)</span>

The membrane time constant $\tau_m = R_m \times C_m$ defines how quickly the neuron’s membrane potential responds to input.

If we increase $\tau_m$, we are effectively **increasing the resistance** (since capacitance is constant).  

That means:

- The neuron **charges and discharges more slowly**,
- But it also **reaches higher voltages** before leaking,
- So it can **fire more spikes** for the same input.
    

**Prediction:** Increasing τₘ → more spikes and slower adaptation  
**Decreasing τₘ** → fewer spikes, faster charging/discharging

### <span style="color:rgb(161, 40, 226)">1.4.3 Absolute Refractory Period</span>

The **refractory period** is the time during which the neuron cannot fire again after a spike.  
If we increase it:

- The neuron stays inactive longer after each spike,
- So the **firing rate decreases** (fewer spikes per unit time).
    

Even though the difference might seem subtle in the plots, it’s a crucial parameter for controlling **spike frequency** and **timing precision** in larger networks.

### <span style="color:rgb(161, 40, 226)">1.4.4 From Single Neurons to Populations</span>

So far, we’ve simulated only **one neuron**.  However, NEST Desktop allows you to:

- Increase the **population size** (e.g. 1000 neurons),
- Observe **collective dynamics**, and
- Study **network-level behavior**.
    
This introduces the possibility of simulating **cortical networks**, composed of:

- ~80% **excitatory neurons**, and
- ~20% **inhibitory neurons**,  
    connected together in structured circuits.

##  <span style="color:rgb(239, 179, 1)">1.5 Poisson Input to Single Neurons</span>
Let’s now replace the **Direct Current (DC)** stimulus with a **Poisson spike generator**.

In biological terms, synaptic input from other neurons arrives as **discrete electrical spikes**, not as a continuous current.  
The **Poisson generator** models this **stochastic (random)** input, simulating the irregular spiking activity that neurons receive from their presynaptic partners.

### <span style="color:rgb(161, 40, 226)">1.5.1. Configuration</span>

To add it:

- From the stimulator list → select **_Poisson generator_**
    
- Set the following parameters:
    
    - **Start time:** 100 ms
    - **Stop time:** 500 ms
    - **Mean firing rate:** determines how frequent the spikes are (e.g. 10 Hz, 100 Hz…)

This generator produces spikes **randomly distributed in time**, following a **Poisson process**, meaning the intervals between spikes are **exponentially distributed**.

### <span style="color:rgb(161, 40, 226)">1.5.2. Understanding the Behavior</span>

![[Pasted image 20251101155521.png]]

Let’s begin with a **10 Hz Poisson input**.  This means that, on average, **10 spikes per second** are generated — but not evenly spaced.  You’ll see that each spike produces a **sharp increase** in the postsynaptic neuron’s membrane potential, followed by a **return to baseline**, following the classic RC decay of the membrane.

Each presynaptic spike is essentially **convolved** with the membrane’s impulse response — a brief depolarization followed by exponential relaxation.
### <span style="color:rgb(161, 40, 226)">1.5.3. Increasing the Firing Rate<br></span>
![[Pasted image 20251101160018.png]]
If we increase the input rate (for example, to **500 Hz**), the postsynaptic neuron receives spikes so frequently that:

- The membrane potential no longer returns to baseline between spikes,
- The response becomes **almost steady**, resembling a **constant depolarization**,
- This mimics what happens when many presynaptic neurons fire asynchronously.

However, in biological reality, **single neurons rarely fire at 500 Hz**.  
Instead, a neuron typically receives input from **many other neurons** (often tens or hundreds), each firing at **moderate rates** (10–20 Hz).

### <span style="color:rgb(161, 40, 226)"> 1.5.4. Simulating Population Input</span>

![[Pasted image 20251101155955.png]]

To model this more realistically, we can:

- Keep the **firing rate** moderate (e.g. 20 Hz),
- But **increase the population size** (e.g. 50 Poisson generators).
    

In this way, the postsynaptic neuron integrates **many independent Poisson inputs**, resulting in:

- A smoother and more continuous depolarization,
- Increased membrane potential fluctuations,
- A higher probability of reaching the firing threshold.
    
### <span style="color:rgb(161, 40, 226)">1.5.5. Summary</span>

| Parameter              | Biological Meaning               | Effect on Membrane Potential   |
| ---------------------- | -------------------------------- | ------------------------------ |
| Firing rate ↑          | More frequent presynaptic spikes | More depolarized, more firing  |
| Population size ↑      | More presynaptic sources         | Smoother and stronger input    |
| Low rate / few neurons | Sparse input                     | Isolated small depolarizations |

## <span style="color:rgb(239, 179, 1)">1.6 Synaptic Connections and Parameters</span>

Up to now, we have seen how to stimulate a single neuron using different types of inputs — either **direct current** or **Poisson-distributed spikes**.  
Now, we move one step further and look at how **neurons are connected** to each other — that is, how the spikes of one neuron influence another.


### <span style="color:rgb(161, 40, 226)">1.6.1 Synaptic Connections in NEST</span>

In **NEST Desktop**, every connection between two nodes (e.g., a Poisson generator and a neuron) has an associated **synapse model**.

If you select either the **Poisson generator** or the **neuron**, you can access the **connection parameters**.  
These define _how_ the presynaptic activity affects the postsynaptic neuron.

### <span style="color:rgb(161, 40, 226)">1.6.2 Connection Types</span>

When connecting neurons, several **connection rules** can be selected:

- **All-to-all:** each neuron is connected to every other neuron.
- **Fixed in-degree:** each neuron receives input from a fixed number (or fraction) of presynaptic neurons.
- **Fixed out-degree:** each neuron projects to a fixed number (or fraction) of postsynaptic neurons.
    
For example:

> If we have 50 neurons and use “all-to-all,” then each neuron connects to all the others.  
> But with a _fixed in-degree_ connection (e.g., 80%), only 80% of the possible presynaptic neurons will connect to each postsynaptic target.

This parameter allows us to **control the density** and **structure** of the network.

### <span style="color:rgb(161, 40, 226)">1.6.3 Synapse Model Parameters</span>

The most common and simple one is the **Static Synapse**, which includes two key parameters:

| Parameter  | Biological Meaning                                                                                             | Effect                                           |
| ---------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| **Weight** | Strength of the synaptic connection — related to neurotransmitter release, vesicle number, or receptor density | Higher weight → stronger postsynaptic response   |
| **Delay**  | Transmission delay between presynaptic spike and postsynaptic response                                         | Longer delay → slower propagation of information |

![[Pasted image 20251101184809.png]]

For example:

> If we increase the **weight** to 5, the postsynaptic neuron will receive stronger depolarizations for each spike arriving from the presynaptic side.

This is analogous to **increasing the efficacy of synaptic transmission**, as if more sodium channels were activated or more neurotransmitter vesicles were released at the synapse.

## <span style="color:rgb(239, 179, 1)">1.7 Other Input Types</span>
Besides the **DC generator** and the **Poisson generator**, NEST provides several other types of **stimulators** that allow us to model neuronal input in different ways.
### <span style="color:rgb(161, 40, 226)">1.7.1 Noise Current</span>

The **Noise Current** (`noise_generator`) provides a continuous current input that _fluctuates randomly_ around a mean value.

- **Mean value (pA):** acts like a DC current — defines the average level of depolarization.
- **Standard deviation (pA):** determines the intensity of the random fluctuations around the mean.
    

This is useful to simulate the **noisy background activity** typically present in the brain due to the large number of ongoing synaptic events.

> 🧠 Biological analogy: spontaneous synaptic bombardment that a neuron receives even without specific stimuli.

### <span style="color:rgb(161, 40, 226)">1.7.2 Spike Generator</span>

The **Spike Generator** allows you to manually define **specific spike times** to deliver to the neuron.

- You specify an **array of spike times** (e.g., `[100, 200, 300]` ms).
    
- Optionally, you can assign **weights** to each spike to define its strength.

![[Pasted image 20251101211410.png]]

~~~
Spike times: [100, 200, 300]
Weights: [100, 100, 100]
~~~

This stimulator produces spikes exactly at those times — deterministic rather than stochastic like the Poisson generator.

 Typically used when reproducing experimentally recorded spike trains, or when testing a model with precisely timed inputs.

### <span style="color:rgb(161, 40, 226)">1.7.3 When to Use Each Input Type</span>

| Input Type            | Description                          | Typical Use                           |
| --------------------- | ------------------------------------ | ------------------------------------- |
| **DC Generator**      | Constant current                     | Simplified deterministic stimulation  |
| **Poisson Generator** | Random spike train with average rate | Realistic synaptic activity modeling  |
| **Noise Current**     | Fluctuating continuous current       | Simulate background synaptic noise    |
| **Spike Generator**   | User-defined precise spikes          | Reproduce experimental spike patterns |

# <span style="color:rgb(223, 109, 109)">2. Hodgkin-Huxley Model Simulation</span>

The **Hodgkin-Huxley (HH)** model is a **biophysical model** of the neuron membrane that describes how **action potentials** are generated through the **opening and closing of ion channels**.

## <span style="color:rgb(239, 179, 1)">2.1 Model Overview</span>

Unlike the **Leaky Integrate-and-Fire** model, which behaves like a simple **RC circuit**, the HH model incorporates **voltage-gated ion channels** for **sodium (Na⁺)** and **potassium (K⁺)**, as well as a **leak channel** that represents passive current flow.

![[Pasted image 20251101211449.png]]

Each channel is described by **differential equations** that model their dynamics through **gating variables**:

- **m(t)** – activation variable for Na⁺ channels
- **h(t)** – inactivation variable for Na⁺ channels
- **n(t)** – activation variable for K⁺ channels

These variables represent the probability that a specific gate is **open** at a given time.

The overall membrane current is determined by:

$$  
I = g_{Na} m^3 h (V - E_{Na}) + g_K n^4 (V - E_K) + g_L (V - E_L)  
$$
where:

- ( $g_{Na}, g_K, g_L$ ) are the maximum conductances,
- ( $E_{Na}, E_K, E_L$ ) are the reversal potentials for each ion species.

### <span style="color:rgb(161, 40, 226)">2.1.1 Biological Meaning</span>

This model reproduces the **shape and timing** of real action potentials very accurately.  
Because it explicitly models channel kinetics, it can be extended to simulate different types of **cells** by adding more channels (e.g., calcium channels in cardiac cells).

> 🧠 In research, this principle is widely used — for instance, in modeling specific channelopathies such as **epilepsy** or **arrhythmia**, where mutations in sodium or potassium channels alter neuronal or cardiac excitability.

### <span style="color:rgb(161, 40, 226)">2.1.2 Implementation in NEST</span>

In **NEST Desktop**, the neuron model can be selected as **“hh_psc_alpha”**, which includes the HH formalism and allows current input stimulation.

**Typical setup:**

- **Neuron model:** `hh_psc_alpha`
- **Stimulus:** Direct current generator (DC)
- **Recorder:** Multimeter (records several variables simultaneously)

### <span style="color:rgb(161, 40, 226)">2.1.3 Recording Variables</span>

The **multimeter** allows you to record:

- Membrane potential (**Vₘ**)
- Sodium activation (**m**)
- Sodium inactivation (**h**)
- Potassium activation (**n**)

You can customize:

- Which variables are displayed
- The color of each trace for clarity

Example:

- $( V_m )$ → blue
- $( m )$ → red
- $( h )$ → green
- $( n )$ → orange

### <span style="color:rgb(161, 40, 226)">2.1.4 Simulation Behavior</span>

![[Pasted image 20251101231827.png]]

Start with a **DC current** of 100 pA (start = 100 ms, stop = 500 ms).  
As you increase the current amplitude:

- At low amplitudes, the neuron stays below threshold → no spike.
- Beyond a certain level, the neuron fires a **true action potential**.
- The shape of the spike shows the **opening and closing sequence** of Na⁺ and K⁺ channels.
    
> This spike is not artificial as in the LIF model — it **emerges naturally** from the biophysical equations.

By displaying $( m, h, n )$ along with $( V_m )$, we can see:

- $( m )$ rises quickly at the onset → Na⁺ channels open.
- $( h )$ slowly decreases → Na⁺ channels inactivate.
- $( n )$ increases → K⁺ channels open, repolarizing the cell.


![[Pasted image 20251101232147.png]]
This interplay generates the full **depolarization–repolarization cycle** of an action potential.

### <span style="color:rgb(161, 40, 226)">2.1.5 Summary</span>

|Model|Description|Output|Key Parameters|
|---|---|---|---|
|**LIF**|Simplified RC circuit|Artificial spikes (reset manually)|τₘ, Vₜₕ, refractory time|
|**HH**|Biophysical ion channel model|Realistic action potentials|gₙₐ, gₖ, Eₙₐ, Eₖ, gating variables (m, h, n)|

## <span style="color:rgb(239, 179, 1)">2.2 Channel Dynamics and Experimental Origins</span>

![[Pasted image 20251102103350.png]]

Once we have the **Hodgkin-Huxley model** set up and visualized, we can observe the **three main gating variables** that define the model’s ion channel behavior:

|Variable|Channel|Meaning|Range|
|---|---|---|---|
|**m(t)**|Sodium (Na⁺)|Activation (opens channel)|0 → 1|
|**h(t)**|Sodium (Na⁺)|Inactivation (closes channel)|1 → 0|
|**n(t)**|Potassium (K⁺)|Activation (opens channel)|0 → 1|

- When **m** increases toward 1 → Na⁺ channels open rapidly, producing the depolarization.
- **h** decreases → Na⁺ channels close (inactivate).
- **n** increases more slowly → K⁺ channels open to repolarize the membrane.

These dynamic variables reproduce the full ionic flow during the **action potential**.

You can also add other recordings, such as the **total excitatory synaptic current**, representing the combined ionic current through all open channels.  
Even though its absolute value is small in this simple simulation, it illustrates how ionic currents add up in a neuron population.

### <span style="color:rgb(161, 40, 226)">2.2.1 Experimental Foundation — The Patch Clamp and the Squid Axon</span>

![[Pasted image 20251102103218.png|400]]
The Hodgkin-Huxley model was originally developed in the **1940s–50s** using the **giant axon of the squid**.  
This axon is large enough (≈0.5–1 mm diameter) to insert electrodes directly, allowing precise electrical recordings.

![[Pasted image 20251102103237.png|400]]
To measure these ionic currents, Hodgkin and Huxley used the **voltage clamp technique** — a precursor to the modern **patch clamp**.

**Voltage clamp principle:**

- The membrane voltage is “clamped” (kept constant) at a chosen value.
- The current required to hold that voltage is measured.
- This current corresponds to the ionic flow through the membrane at that voltage.
    

Different configurations of the **patch clamp** allow measurements of:

- Whole-cell currents,    
- Single-channel activity,
- Or intracellular ion concentration changes.

### <span style="color:rgb(161, 40, 226)">2.2.2 What They Observed</span>

When the researchers applied **voltage steps**, they recorded three characteristic responses:

![[Pasted image 20251102103435.png|400]]
1. A fast, **capacitive current** — brief charge movement on the membrane.
2. A **transient inward current** — carried by Na⁺ ions.
3. A **delayed outward current** — carried by K⁺ ions.

By varying the clamped voltage (from hyperpolarized to depolarized values), they could see how the amplitude and timing of each current changed.

## <span style="color:rgb(239, 179, 1)">2.3 Reproducing the Experiment in Simulation</span>

In our NEST Desktop setup, we use **current clamp** (injecting current), not **voltage clamp**, so we do not directly see the isolated ionic currents — only the resulting **membrane potential**.

However, we can conceptually reproduce what Hodgkin and Huxley did:

> **Goal:** Simulate the effect of blocking specific ion channels.

They achieved this experimentally by using:

![[Pasted image 20251102103539.png]]

- **Tetrodotoxin (TTX)** → blocks Na⁺ channels.
- **Tetraethylammonium (TEA)** → blocks K⁺ channels.
    

In the simulation, we can achieve the same effect by adjusting the **maximum conductances**:

|Channel|Parameter|Effect if Reduced|
|---|---|---|
|Sodium|( g_{Na} )|Reduces or blocks depolarizing inward current|
|Potassium|( g_K )|Reduces or blocks repolarizing outward current|

Try the following:

1. Start from the default HH neuron.
2. Gradually reduce ( $g_{Na}$ ) — observe that the **depolarizing spike disappears**.
3. Then reduce ( $g_K$ ) — observe that **repolarization becomes slower**, and the membrane stays depolarized longer.
4. Set both to zero — the neuron becomes **electrically passive**, showing no spiking behavior.
    

This mirrors the **original experimental logic**:

- Block one current → identify its contribution to the total membrane behavior.
- Fit equations to describe the dynamics of each channel separately. 
#### Key Insight

> The Hodgkin-Huxley model is not just a theoretical construct — it’s an **empirical synthesis** of electrophysiological recordings and mathematical fitting.

It provides the foundation for almost all modern neuron models, which simply extend its structure with additional channels or compartmental geometry.


## <span style="color:rgb(239, 179, 1)">2.4 Summary: Using Complex Neuronal Models (Hodgkin-Huxley)</span>

### <span style="color:rgb(161, 40, 226)">2.4.1. Purpose of the Model</span>

- The Hodgkin-Huxley model allows us to **accurately reproduce the biological mechanisms** of real neurons.
- Ionic channels (sodium and potassium) are **explicitly modeled** through activation and inactivation variables.
- This makes it possible to simulate **realistic responses** to electrical stimuli — unlike simpler models such as the _leaky integrate-and-fire (LIF)_ model.
    
### <span style="color:rgb(161, 40, 226)">2.4.2. Model Flexibility</span>

- You can **add more channels** (e.g., calcium or slow adaptation currents) to simulate different types of neurons.
    
- Different channel combinations → **different neuronal behaviors**, such as:
    
    - Adaptive firing (the neuron’s firing rate decreases over time),
    - Rebound spiking (a spike occurs after a hyperpolarizing stimulus),
    - Bursting behavior (multiple spikes in quick succession).


### <span style="color:rgb(161, 40, 226)">2.4.3. Example Phenomenon: Rebound Response</span>
![[Pasted image 20251102110213.png]]
- When applying a **hyperpolarizing stimulus** (negative current):
    - In the Hodgkin-Huxley model, sodium channels become **inactivated**, and potassium channels **open** to restore the membrane potential.
        
- When the stimulus ends:
    - The sudden change in activation/inactivation causes a **depolarizing rebound**, leading to a **rebound spike**.
        
- This behavior **cannot be reproduced** with the LIF model, since it lacks explicit ion channel dynamics.
    
### <span style="color:rgb(161, 40, 226)">2.4.3 Physiological Interpretation</span>

![[Pasted image 20251102110858.png]]

- During hyperpolarization:
    
    - 🔹 **Na⁺ channels** → closed/inactive
    - 🔹 **K⁺ channels** → open (trying to bring the potential back to equilibrium)
        
- When the stimulus stops:
    
    - A sharp change in the gating variables (activation/inactivation) produces a **depolarizing current**, causing the rebound spike.
        
- This reflects the **real ionic balance** described by the **Nernst potential** (≈ –90 mV for potassium).

### <span style="color:rgb(161, 40, 226)">2.4.5. Conclusion</span>

- The Hodgkin-Huxley model lets us **observe internal variables directly**, such as the probabilities of ion channel opening and closing.
    
- It provides a **complete understanding** of how electrical stimuli translate into action potentials and how the neuron **adapts or reacts** to them.
    
- Although more complex to code, it offers **high biological fidelity**, making it extremely valuable for computational neuroscience.

  
# <span style="color:rgb(223, 109, 109)">3. Spike-Timing Dependent Plasticity (STDP) — Concept and Simulation</span>

## <span style="color:rgb(239, 179, 1)">3.1 What STDP Is</span>

![[Pasted image 20251102113500.png]]
- **STDP (Spike-Timing Dependent Plasticity)** is a form of _synaptic plasticity_ — a mechanism by which connections between neurons (synapses) change their strength over time.
    
- The change depends on the **relative timing** between:
    
    - The **presynaptic spike** (the spike from the input neuron), and
    - The **postsynaptic spike** (the spike from the receiving neuron).
        
In short:

- If the **presynaptic spike** occurs **slightly before** the postsynaptic spike → **Long-Term Potentiation (LTP)** → the connection **strengthens**.
    
- If the **presynaptic spike** occurs **after** the postsynaptic one → **Long-Term Depression (LTD)** → the connection **weakens**.
    

This timing-based learning rule allows neural circuits to **self-organize** and encode patterns — it’s the biological basis for learning and memory.


## <span style="color:rgb(239, 179, 1)">3.2 Simplified Modeling of STDP in NEST</span>

- In NEST, STDP can be simulated with **predefined synapse models**, such as the `"stdp_synapse"` model.
    
- The change in synaptic weight follows an **exponential curve** depending on the timing difference (Δt) between pre- and post-synaptic spikes.
    
    - One exponential function governs **potentiation (Δt > 0)**.
    - Another governs **depression (Δt < 0)**.
        

Even though more complex versions exist (e.g., involving neurotransmitter concentration, neuromodulators, etc.), this simple exponential model is enough to capture the **core time-dependent learning rule**.

## <span style="color:rgb(239, 179, 1)">3.3 Network Setup</span>

In the simulation example:

![[Pasted image 20251102113602.png]]
- There are **two neurons** (e.g., _Integrate-and-Fire_ type).
- A **spike generator** sends identical spikes to both neurons.
- A **connection** is created **from Neuron 1 (presynaptic)** to **Neuron 2 (postsynaptic)**, using the **STDP synapse** model.

A **delay** is introduced so that the spikes don’t reach both neurons simultaneously — this time difference (e.g., 10 ms) is what determines whether the weight will **increase or decrease**.


### <span style="color:rgb(161, 40, 226)">3.3.1 Configuring the STDP Synapse</span>

![[Pasted image 20251102113644.png]]
After importing the model in NEST:

- Change the **connection type** between Neuron 1 and Neuron 2 from `static_synapse` → `stdp_synapse`.
    
- Inside the connection settings, you can modify:
    
    - `weight`: the initial synaptic strength.
    - `delay`: time between pre- and post-synaptic spikes.
    - `alpha`: asymmetry parameter (controls the balance between LTP and LTD).
    - `tau_plus` and `tau_minus`: time constants for potentiation and depression windows.
        
### <span style="color:rgb(161, 40, 226)">3.3.2 Expected Results</span>

![[Pasted image 20251102113720.png]]
- When simulating, the **presynaptic spikes** (blue) and **postsynaptic spikes** (orange) are recorded.
- Over time:
    
    - The **synaptic weight increases** gradually as the spikes occur with consistent timing (potentiation).
    - If the spike timing were reversed, you’d expect **depression** instead (but in this demo, only potentiation is shown).
        
- Higher **frequency** of stimulation leads to stronger weight changes — because more coincident spikes mean stronger learning.
    
### <span style="color:rgb(161, 40, 226)">3.3.3 Biological Meaning</span>

- This mechanism mimics how **real neurons learn from experience**:
    
    - Repeated, well-timed activation strengthens connections (learning).
    - Poorly timed activation weakens them (forgetting or inhibition).
        
- Over time, such local timing rules can lead to **global network reorganization** and pattern recognition, just as in artificial neural networks.
    

## <span style="color:rgb(239, 179, 1)">3.4 Suggested Exercises</span>

To explore how STDP behaves:

- 🔹 **Change the initial weight** — observe how it affects the amplitude of the postsynaptic response
- 🔹 **Modify the delay** between spikes — see when potentiation turns into depression.
- 🔹 **Adjust `tau_plus` or `alpha`** — these control how fast or how strong the learning curve is.
- 🔹 **Vary the spike frequency** — check how faster stimulation enhances the effect.
    

## <span style="color:rgb(239, 179, 1)">3.5 Summary</span>

STDP is a biologically realistic rule for synaptic learning, where:

> **Δt (timing difference) → determines Δw (weight change)**

In NEST, by adjusting the **timing**, **delay**, and **synaptic parameters**, you can simulate how neural connections **adapt and learn** over time — a core principle that bridges **biological neuroscience** and **artificial neural networks**.
