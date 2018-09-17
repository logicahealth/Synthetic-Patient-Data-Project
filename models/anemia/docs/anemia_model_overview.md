# Anemia Model Overview

### Model State As Of 15-Sep-2018

There are two JSON modules that implement the model:

* `anemia__unknown_etiology`
* `anemia_sub`

Model execution starts with `anemia__unknown_etiology`, which first partitions the population using race, gender, and prevalence information obtained from the initial research (see `research\Anemia percentages ABBOTT`). 

This is a very complex partitioning of the population.  A partial view of the race/gender/prevalence partitioning is:

![Anemia Partitioning](images\PopBranches.png)

Most of the population will not develop *unknown etiology* anemia and will therefore not participate in the model.  For those who will develop anemia, time delays are used to distribute anemia onset into the following age groups:

* 0 - 14 years
* 15 - 49 years
* 50 - 79 years
* 80 - 85 years

A feature request logged in the *Synthea* project could dramatically simplify this complex branching via the use of table-based population distribution.   This feature has an unknown completion timeframe.

Simple anemia symptoms (such as tachycardia, shortness of breath, and fatigue are then generated) for the anemia population, and an encounter is also generated that surrounds the generation of further anemia complications:

![Encounter](images\Encapsulating Encounter.png)



The `anemia_sub` module is called to generate a large amount of detail for the patient, starting with a condition onset event that generates *SNOMED-CT 271737000: Anemia (disorder)*.

Gender and probability based decisions are then used to generate blood panels (routine and severe for each gender), followed by a review of systems, medication re-conciliation, and a brief examination.  The sub-module also attempts to handle in-patient encounters, transfusions, and medication administration.

The sub-module is incomplete and contains the following TBD sections:

* Collection of social habits
* Collection of nutrition information
* Generation of additional severe anemia events
* Generation of additional simple anemia events (perhaps additional medications or treatments)

The model is not yet verified.  Initial patient generation revealed that the generated population anemia percentages did not match those given by the model, so additional testing / model correction work is likely necessary.