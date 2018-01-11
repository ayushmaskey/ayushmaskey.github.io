
## increase volume in hyperV cluster
 * shutdown vm
 * increase volume in SAN
 * failover --> storage --> disk --> right click --> maintenance mode
 * computer management --> disk management --> extend volume
 * hyperV --> select vm --> right click --> setting --> find the path of the vhd files
 * hyperV --> select vm --> edit disk --> find the vhd --> extend
 * turn on vm
 * vm --> computer management --> disk management --> extend volume