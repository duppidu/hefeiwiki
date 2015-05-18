Explo Communication
===================


####Communication between Classes and Explo handler in Explo Phase :
(Sequence Diagramm Look in: https://stackedit.io/editor)
Surround with:
//```sequence
....

//```

------------

```sequence
Refbox->ExploControll: Send Fields (-Z1-Z2...)
Note right of ExploControll: getCoord
Note right of ExploControll: StartPoint For Next Machine
ExploControll->Waycontroller: sendTarget(/robo/local/pos/target)
Note right of Waycontroller: goTarget()(Coord)
Waycontroller->ExploControll: inPos(to define)(String with true/false)
ExploControll->Waycontroller: Explore(String with explore)
Waycontroller->ExploControll: CoordIn()(Coord)
Waycontroller->ExploControll: CoordOut()(Coord)
Camera->ExploControll: get Id, Color
ExploControll->Refbox: SendMachine(Machine)(to define)
ExploControll->MasterBroker: SendMachine(Machine)(to define)
Note right of ExploControll: go to Start until finished
```

This Cycle will pass 2 times, on each of the 3 Robotinos. As This Cycle is finished The Field
With its Machines should be complete on each Robotino and Transmitted to the Refobx