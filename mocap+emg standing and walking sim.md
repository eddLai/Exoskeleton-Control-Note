[[SCONE]]

7 Days
1. make model fit an object
	2. mocap data input: 
		1. [ ] API automatically do: 
			1. [ ] `.trc` -> opensism IK 
			2. [ ] opensism IK -> `.mot`
			3. [ ] `.mot`-> `_q.sto`
			4. [ ] optimizing
			5. [ ] optimizing -> trained weights
			6. [ ] go back to 1. with trained weights
		2. [ ] Full body muscle skeleton model (opensim creator)
		3. [ ] points lost issue, interpolation?
	3. EMG data input
		1. [ ] difference between our EMG data and Gold standard
			1. quantize the level of fatique from EMG
		2. [ ] opensim [SO](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53085189/Working+with+Static+Optimization), [CMC](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53088683/Example+-+Computed+Muscle+Control ) -> muscle activation
		3. - [ ] into Scone controller parameters like tension and length, possible?
	4. `_q.sto` Scone mimic measure
		1. Training is Scone
		2. Meaning of the muscle .activation in scone
		3. Transform the Real EMG to muscle activation
2. Validation by collect a new data