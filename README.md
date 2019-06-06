# AWS Cloud Practitioner Essentials (Second Edition)


## Cloud

* Regios 
    * AWS servers located all over the globe
    * Each region is a separete geographic area that has multiple isolated locations **known as availability zones**

* Availability zones
    * One or more discreet datacenters
    * Contains redundant power, network, and connectivity
    * House in separete facilities 

* Fault-tolerant: System remains available in case part of it fails (CAP theorem)
    * Redundancy 


* Security

    * The customer decides the region systems will be deployed
    * Ownership of data
    * How do you handle encryption and encryption keys

## Interface

* Three ways to use AWS
    * AWS CLI
    * AWS Management Console (browser)
    * Software Developer Kits (SDKs)

    * ![aws](./images/1.png)

    * Each user (IAM) can create Resource Groups
        * A resource group is a group of AWS services (dashboard)
    
    * You can also tag resources in order to do a quick search later (tag is key/value)

# Core Services

* Elastic Cloud Compute (EC2)

    * Instances
        * Pay as you go
        * Broad selection of hardware and software 
        * Global hosting (many regions)
    

    * Setup
        * Login to AWS Console
        * Choose a region
        * Launch EC2 Wizard
        * Select AMI
            * Amazon Machine Image (Software)
        * Instance type (Hardware)
        * Configure network
        * Configure storage
        * Configure key pairs 
        * Launch and connect

* EBS (Elastic Block Store)

    * Storage unit for EC2 instance
    * Choose HDD or SSD
    * Persistent and customizable block storage for EC2 instances
    * Replicated in the same Availability Zone

    * Backup using snapshots
        * Share snapshots or even copy snapshots to a different aws region (Virginia to Tokyo)

    * Easy and transparent Encryption
        * Encrypt data between EC2 instance and EBS inside Amazon networks without extra cost
    * Elastic volumes

    * Availability
        * Data in a volume is automatically replicated in multiple server at the availability zone
    
    * You can do resize operations on the fly (from 60gb to 100gb, from hdd to ssd)
        * No need to stop the instances
    
    * EC2 Instance must resign in the same availability zone and region as EBS instance for the connection to be made

    * `lsblk`: List block devices (hard drives)
        * `lsblk` lists information about all available or the specified block
       devices.  The lsblk command reads the sysfs filesystem and udev db to
       gather information. If the udev db is not available or lsblk is
       compiled without udev support than it tries to read LABELs, UUIDs and
       filesystem types from the block device. In this case root permissions
       are necessary.
    
    * `mke2fs /dev/xvdb`: `xvdb` in this case is the new block device attached to the EC2 instance 
        * Will create a file system on this volume
        * `mount /dev/xvdb /mnt`: Mounting file system inside `/mnt`
            * `unmount /mnt`: Now I can detach the volume from my instance 
    
    * You can drill down your bill per tags
        * Tags are relevant

* Amazon Simple Storage Service (S3)

    * Managed cloud storage service 
    * Store virtually unlimited number of objects
    * Access any time, any where
        * http, and https
    * Rich security controls
        * None of your data is shared publicly by default 

    * The data stored inside a bucket is replicated at many other facilities inside the AWS region

    * Common Use Cases
        * Storing application assets
            * media files
            * logs
            * images
        * Static Web Hosting 
        * Backup and disaster recovery
            * Supports cross region replication
        * Staging area for Big data
            * Amazon Redshift 
        * Many more...
    
    * Bucket name must be DNS compliant 
    * AWS CLI

        * `aws s3 cp demo.txt s3://amazing-bucket-1/hello.txt`
        * `aws s3 sync some-folder s3://amazing-bucket-1/files`
            * Sync an entire folder with s3
        
        * Inside an EC2 instance

            * Remember to have the correct IAM access / policy to access the bucket 

            * `aws s3 ls s3://amazing-bucket-1 --recursive`
                * List all files (even inside directories) inside bucket `amazing-bucket-1`
            
            * `aws s3 cp s3://amazing-bucket-1/hello.txt .`
                * Copy txt file from bucket to desktop
                * You could also do the `sync` command in reverse
        

* AWS Global Infrastructure

    * Regions
        * Geographic areas that hosts two or more Availability zones
        * Resources in one regions are not automatically copied to other regions 
        * **Not all services are available at all regions**
    * Availability zones
        * Availability zones are phisically distinct, separate from one to another, but they are connected by a low latency network
        * The get support from different energy source providers and internet providers (tier-1)
        * If one zone goes down, the other ones can handle requests (fault-tolerant)
    * Edge locations
        * CDN - Clound Front
            * Content Delivery Network
        * Request for content is automatically routed to the nearest edge location, so the content is delivered faster to the end users.

* Amazon Virtual Private Cloud (VPC)

    * A private, virtual network in the AWS Cloud
        * Uses same concepts as on premise networking
    * Allows complete control of network configuration
        * Ability to isolate and expouse resources inside VPC