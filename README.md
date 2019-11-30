# csc458a2Bufferbloat

Instructions: sudo ./run.sh

bb-q20
    average: 0.526233333333
    standard deviation: 0.103895679517
    
bb-q100
    average: 1.17904761905
    standard deviation: 0.541145564097
    
questions:
1. Why do you see a difference in webpage fetch times with short and large router buffers?

    In the case of buffer size of 100 packets, TCP continues sending packets with increased cwnd. On the other hand, when the buffer size is 20 packets, packets are considered dropped and cwnd is decreased, so resending the dropped packets may take even more time than keeping more packets waiting in the buffer.

2. Bufferbloat can occur in other places such as your network interface card (NIC). Check the output of ifconfig eth0 on your VirtualBox VM. What is the (maximum) transmit queue length on the network interface reported by ifconfig? For this queue size, if you assume the queue drains at 100Mb/s, what is the maximum time a packet might wait in the queue before it leaves the NIC?
    
    max transmit queue length is 1000 packets and MTU is 1500 B ->
    1000 packets * 1500 B * 8b / (100 * 10 / 6 b/s) = 0.12s.

3. How does the RTT reported by ping vary with the queue size? Write a symbolic equation to describe the relation between the two (ignore computation overheads in ping that might affect the final result).

    RTT is the sum of buffer size over rate of bottleneck link and min RTT ->
    RTT = buf_size / 1.5 mb/s + 20ms, so RTT is proportional to the queue size.

4. Identify and describe two ways to mitigate the bufferbloat problem.

    One way to mitigate the bufferbloat could be decreasing the timeout value for TCP, which would result in the decrease of the cwnd, since pacets stuck in longer queue would be considered dropped. Another way would be setting buffer size based on the local network condition, which could effectively reduce the wait time and handle TCP congestion control better.
