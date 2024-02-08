### What is Sharding and why do we need it?

It is a method for distributing a single dataset across multiple databases, which can then be stored on multiple machines. We need sharding in a DB where number of rows are large. 
CPU cores are involved in reading and writing data to DB via DB drivers. If number of read and write operations increase in a DB, all the CPU cores will be engaged most of the times. So we split the data on multiple db servers and keep those DB servers on multiple machines. Now parallelism can be attained using n CPUs.

### What is Replication and why do we need it?
It is the process of creating replicas to store multiple copies of the same data. The data may or may not be present on different machines.
This setup is also called Master-Slave archtectue whic is discussed later.

It helps in :

- Redundancy of the data
- Speeds up the process of reading and writing
- Reduces load on the databases


<img width="762" alt="image" src="https://github.com/MadhuKashyap/DBConcepts/assets/40714383/1654e70e-2668-4b21-8f1a-6ebdd4152ac2">

### Why is SQL DB not feasible for Horizontal Scaling?
Scaling SQL DB horizontally means, keeping 2 replicas of the same DB on 2 different machines such that incoming requests are distributed among them equally using a load balancer.
Now suppose Account table is kept on both machines, if we have 2 subsequent write and read operations of a person's money deposit and check balance query, both the requests will be routed to 2 different machines and discrepancy will happen whih is against ACID property.

This scenario can be easily handled by NO-SQL based cassandra DB using internally implemented logic. Operations are done using routing key so all operations for 1 account holder will happen on 1 machine only

### What is ACID property?
- Atomicity : The entire transaction takes place once or does not happen at all.

Consider the following transaction T consisting of T1 and T2: Transfer of 100 from account X to account Y.  
<img width="698" alt="image" src="https://github.com/MadhuKashyap/DBConcepts/assets/40714383/a610943a-529e-4dc8-ba42-dc284f1b0a22">

If the transaction fails after completion of T1 but before completion of T2.( say, after write(X) but before write(Y)), then the amount has been deducted from X but not added to Y. This results in an inconsistent database state.

- Consistency : This means that integrity should be maintained before and after transaction
Total before T occurs = 500 + 200 = 700. 
Total after T occurs = 400 + 300 = 700. 


- Isolation : Multiple transactions occur independently without interference. In other words, Changes occurring in a particular transaction will not be visible to any other transaction until that particular change in that transaction is written to memory or has been committed. 

Consider two transactions T and T”. 
<img width="627" alt="image" src="https://github.com/MadhuKashyap/DBConcepts/assets/40714383/497c965c-e978-4764-b6a5-ef4a78ed747d">

Suppose T has been executed till Read (Y) and then T’’ starts. As a result, interleaving of operations takes place due to which T’’ reads the correct value of X but the incorrect value of Y and sum computed by 
T’’: (X+Y = 50, 000+500=50, 500) 
is thus not consistent with the sum at end of the transaction: 
T: (X+Y = 50, 000 + 450 = 50, 450). 
This results in database inconsistency, due to a loss of 50 units.

- Durability : This property ensures that once the transaction has completed execution, the updates and modifications to the database are stored in and written to disk and they persist even if a system failure occurs.


### What is Master-Slave architecture in DB?

### What is the difference between SQL and NoSQL DBs?

### Which DB to use in what scenario?


