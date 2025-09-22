In the model there are two different antibiotics that can be used by doctors in the hospital, drug A and drug B.
The bacteria can have four different types:
Sensitive to both antibiotics (sensitive)
Resistant to drug A and sensitive to drug B (resistant_A)
Resistant to drug B and sensitive to drug A (resistant_B)
Resistant to both drugs (resistant_AB).
Drug A is better at killing the bacteria, helping patients clear their infection twice as fast as drug B when the infecting bacteria are sensitive to it (efficacy drug A = 0.01, effiacy drug B = 0.005).
Both drugs carry a cost of resistance for the bacteria.
The infection is potentially lethal, with each infected patient having a 1% chance of dying each day.
The model will simulate 5,000 days every time that you run it.
Each simulation will begin with only sensitive bacteria, but resistance to both drugs will begin to appear by mutation.
How fast resistance to each drug will spread will depend on how antibiotics are allocated during the simulation.
