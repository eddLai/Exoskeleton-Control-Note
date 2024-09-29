[[SCONE]]

7 Days
1. make model fit an object
	2. mocap data input: 
		1. [ ] API automatically do: eddlai
			1. [ ] `.trc` -> opensism IK 
			2. [ ] opensism IK -> `.mot`
			3. [ ] `.mot`-> `_q.sto`
			4. [ ] optimizing: mimic measure
			5. [ ] optimizing -> trained weights
			6. [ ] go back to 1. with trained weights
		2. [ ] Long Head Biceps femoris muscle model
		3. [ ] (Full body muscle skeleton model (opensim creator) sean)
		4. [ ] (points lost issue, interpolation? sean)
	3. EMG data input
		1. [ ] difference between our EMG data and Gold standard
		2. [ ] 安於data
			1. [ ] quantize the level of fatique from EMG?
		3. Transform the Real EMG to muscle activation
			1. [ ] mocap opensim [SO](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53085189/Working+with+Static+Optimization), [CMC](https://opensimconfluence.atlassian.net/wiki/spaces/OpenSim/pages/53088683/Example+-+Computed+Muscle+Control ) -> muscle activation
			3. [ ] meaning of muscle activation in opensim and scone 
				1. [ ] read the papers
		4. [ ] into Scone controller parameters like tension and length, possible?
2. Validation by collect a new data

Full body, 11初過後再說