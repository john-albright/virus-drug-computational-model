# Virus Proprogation And Drug Computational Model 

This project was completed as to fulfill the requirements for problem set 3 of [MIT 6.00.2x Introduction to Computation Thinking and Data Science](https://online-learning.harvard.edu/course/cs50-introduction-computer-science?delta=0). The starter code for problem set 3 can be found at this [EdX](https://courses.edx.org/assets/courseware/v1/b79fcf3fba22dd033dd933c0ce9c1bc7/asset-v1:MITx+6.00.2x+1T2021+type@asset+block/ProblemSet3.zip) link. A live version of the application can be found on [Replit](https://replit.com/@john-albright/virus-drug-computational-model). The project was built using OOP principles and the pylab interface of the [Matplotlib library](https://matplotlib.org/). There are two main classes SimpleVirus and Patient. Two child classes inherit from these: ResistantVirus and TreatedPatient. The classes have the following instance variables and methods. A custom exception called NoChildException is an error raised in the reproduce() method if the virus does not reproduce. 

SimpleVirus
- constructor requiring two variables: 
  - maxBirthProb (maximum reproduction probability)
  - clearProb (maximum clearance probability)
- getMaxBirthProb(): getter for the maxBirthProb variable
- getClearProb(): getter for the clearProb variable
- doesClear(): simulates a stochastic event to determine whether the current instance of the class "survives"
- reproduce():
  - accepts a variable called popDensity (calculated and used in the update() method of Patient)
  - simulates a stochastic event to determine whether the current instance "creates" a new instance of the class

Patient 
- constructor requiring two variables: 
  - viruses (a list of SimpleVirus or ResistantVirus)
  - maxPop (the virus "capacity" of the patient)
- getViruses(): getter for the viruses variable
- getMaxPop(): getter for the maxPop variable
- getTotalPop(): calculates the number of viruses "in" the patient
- update(): moves one timestep into the future checking if each virus will reproduce or die

ResistantVirus
- constructor requiring four variables:
  - maxBirthProb (inherited)
  - clearProb (inherited)
  - resistances (dictionary of drug name keys mapped to boolean values)
  - mutProb (probability of virus mutating)
- getResistances(): getter for the resistances variable
- getMutProb(): getter for the mutProb variable
- isResistantTo(): accepts a drug name as a variable and gets the boolean value its mapped to
- reproduce(): overridden method of the parent class that factors in the resistances of the virus in determining its reproducibility — the mutateProb determines if the "children" of the virus are resistant to the list of drugs in the resistances dictionary 

TreatedPatient
- constructor requiring the same two variables as its parent but also initializes a list called prescriptions (instance variable that is empty upon instantiation)
- addPrescription(): adds a new drug to the list of prescriptions (if not already in the list)
- getPrescriptions(): getter for the prescriptions variable
- getResistPop(): uses the getter of the ResistantVirus class to determine the population of viruses 
- update(): overriden method that calculates the virus population after one time step (while taking into account the drugs in the prescription list of the TreatedPatient and the resistances dictionary of the ResistantVirus)

The main method calls the two functions simulationWithDrug and simulationWithoutDrug, which create a graph showing how the computational model fares over time. These two graphs are in the screenshots folder. Feel free to create your own simulations.