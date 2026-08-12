**Key Takeaway point**

Amazon EBS
EBS = Elastic Block Store

If the EC2 instance is stopped, the EBS volumes normally remain attached and the data remains intact.

If the EC2 instance is terminated
For the root EBS volume, the default DeleteOnTermination setting is normally true.
Additional/non-root EBS volumes can be configured with DeleteOnTermination=false, 
in which case they remain after the instance is terminated.

EBS is not automatically a backup.

If you accidentally delete the EBS volume, corrupt the filesystem, or suffer some other failure, simply saying "it's EBS" doesn't mean your data is protected.

For backup/recovery, you can create:
EBS Snapshots

EBS Volume: Block storage actively attached to an EC2 instance.

EBS Snapshot: Point-in-time backup of an EBS volume that can be used to restore/create another volume.

The major EBS volume families
Type	Best suited for
gp3	General-purpose workloads; excellent default choice
gp2	Older general-purpose SSD option
io2	High-performance, high-IOPS workloads such as critical databases
st1	Throughput-intensive workloads
sc1	Infrequently accessed, throughput-oriented workloads

The easiest way to understand them is: st1 and sc1 are both HDD-based and designed for large amounts of sequential data, 
but st1 is for data you access more regularly, while sc1 is for data you access rarely.
st1 is designed for applications that need to read/write large amounts of data continuously, especially sequentially.
sc1 is designed for large amounts of data that you don't access very often.
