用於產生generalized forces
mass, force and acceleration，$F = ma$
the net forces and torques at each joint which produce the movement.

**subject01_simbody.osim**: adjusted virtual markers.

$$\begin{equation}
    \mathbf{M}(\mathbf{q}) \ddot{\mathbf{q}} + \mathbf{C}(\mathbf{q}, \dot{\mathbf{q}}) + \mathbf{G}(\mathbf{q}) = \boldsymbol{\tau}_{generalized\ forces}
\end{equation}
$$
$$\mathbf{q}, \dot{\mathbf{q}}, \ddot{\mathbf{q}} \in \mathbb{R}^N$$
$$\mathbf{M}(\mathbf{q}) \in \mathbb{R}^{N \times N}$$
$$C function$$is the vector of 
- Coriolis forces: 運動方向的軸上產生的力
- centrifugal forces: 離心力

更多生物力學:[Biomechanics of Movement – By Thomas K. Uchida and Scott L. Delp](https://biomech.stanford.edu/)


command:`id -S subject01_Setup_InverseDynamics.xml`
Point Force, Body Force

### XML setting
`<results_directory>`
`<model_file>`
`<time_range>`
`<forces_to_exclude>`
`<external_loads_file>`
`<coordinates_file>`
`<lowpass_cutoff_frequency_for_coordinates>`
`<output_gen_force_file>`