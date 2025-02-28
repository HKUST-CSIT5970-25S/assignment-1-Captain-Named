[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Mingen Zheng
### Student Id: 21126390
### Email: mzhengap@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > - Name of measurement tool:
    >   - compress-7zip
    >       - to test the CPU processing capabilities by simulating real-world compression/decompression tasks
    >       - results in the form of x MIPS representing in average x million instructions are executed per second
    >   - ramspeed
    >       - copy + integer
    >          - to leverage efficiency of copying integers as the measurement of ability of ram reading and writing
    >          - results in the form of x MB/s representing the data amount copied per second
        

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |     3506/3050MIPS    |   11117.00 MB/s    |
    | `t2.medium`  |   10072/5929MIPS     |  19308.75 MB/s      |
    | `c5d.large` |   7476/4934MIPS   |    13695.12 MB/s   |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.
    - Yes, the performance of EC2 instances increases commensurate with the increase of the number of vCPUs and memory resource. t2.medium and c5d.large have 2 vCPUs and 4G Mem, which is better than t2.micro with 1 vCPU and 1G Mem. Consequently t2.medium and c5d.large perform better than t2.micro.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | [3.70K] Mbits/sec | 0.247 ms |
    | `m5.large` - `m5.large`   | [8.50K] Mbits/sec | 0.294 ms |
    | `c5n.large` - `c5n.large` | [4.96K] Mbits/sec | 0.163 ms |
    | `t3.medium` - `c5n.large` | [2.26K] Mbits/sec | 0.680 ms |
    | `m5.large` - `c5n.large`  | [4.95K] Mbits/sec | 0.139 ms |
    | `m5.large` - `t3.medium`  | [2.05K] Mbits/sec | 0.794 ms |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.
    - From connections between 2 same-type VMs, we can conclude that the order of nerwork performance is: m5.large > c5n.large > t3.medium.
    - From connections between 2 different-type VMs, we can conclude that in this case the performance bottlenecked by the weaker one of the two.
2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | [32.9] Mbits/sec |  62.2 ms |
    | N. Virginia - N. Virginia | [4.78K] Mbits/sec | 0.285 ms |
    | Oregon - Oregon           | [8.99K] Mbits/sec | 0.111 ms |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
    - VMs in the same region communicate faster and VMs in different rigeons communicate much more slowly.
