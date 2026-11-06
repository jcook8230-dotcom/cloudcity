**cluster** cluster instances into low latency group in a single availability zone 
 ![[Pasted image 20261104120523.png]]
**spread** spread instances across underlying hard ware max 7 instances per group per az. critical 
applications

![[Pasted image 20261104120608.png]]
**partition** spread instances across many different partitions which rely on different sets of racks within an az. scales to 100s of ec2 instances per group Hadoop Cassandra Kafka
![[Pasted image 20261104120659.png]]

**precision** time direct access to high precision time sources 
![[Pasted image 20261104121136.png]]