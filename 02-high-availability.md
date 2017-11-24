# High Availability

## In Brief

* AWS services are infinitely scalable. 
* Difference between Elastic and Scalable.
* Knowing when to scale up (vertical) or scale out (horizontal).
* RDS Multi-AZ
* RDS Read Replicas (and the difference between them and M-AZ setups)

## Infinitely Scalable

## Elastic vs Scalable

## Scale Up or Scale Out

* Archetecting for scaling out allows for better elasticity.
  * Using only compute power required for the task. Not paying for unused CPU.

## RDS Multi-AZ

* Sets up read-replica RDS instance in another AZ in the same region in a different subnet.
  * All regions have at least 2 AZs. Some more.
* Force failover to different AZ by rebooting instance.
* Refer to instance by hostname, not by individual IP. 
  * AWS handles failover. No change of DNS required by us.
* Required for production workloads. Datacentres sometimes do catch fire!

## RDS Read Replica

* Creates 'following' database of the same type in a different AZ **or region entirely.**