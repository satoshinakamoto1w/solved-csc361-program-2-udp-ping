Download Link: https://assignmentchef.com/product/solved-csc361-program-2-udp-ping
<br>
In this lab, you will learn the basics of socket programming for <strong>UDP</strong> in Python. You will learn how to send and receive datagram packets using UDP sockets and also, how to handle UDP packet <strong>retransmissions</strong>. Throughout the lab, you will gain familiarity with a Ping application and its usefulness in computing statistics such as packet loss rate.

You need to be familiar with the standard ping protocol <strong>Internet Control Message Protocol</strong>

ICMP available in modern operating systems first. The ping protocol allows a client machine to send a packet of data to a remote machine, and have the remote machine return the data back to the client unchanged (an action referred to as echoing). Among other uses, the ping protocol allows hosts to determine round-trip times to other machines.

Then you are required to implement these functionalities using a simpler protocol, UDP, rather than the standard ICMP to communicate between a client and a server. You are given a skeleton code for the Ping server pingserver.py . Your task is to complete the Ping server code first and then design and implement your Ping client ( pingclient.py ).

<h1>Server Code</h1>

<h2>Server sample code</h2>

You are provided a skeleton code for the Ping server. You are required to complete the skeleton code pingserver.py first. The places where you need to fill in code are marked with ??????????? . Each place may require one or more lines of code. (<strong>Note:</strong> You may modify pingserver.py any way you like, as long as it meets the following requirements. You may

even ignore this sample code and start all over from scratch.)

<h2>Functionalities of your server</h2>

UDP provides applications with an unreliable transport service. Messages may get lost in the network due to router queue overflows, faulty hardware or some other reasons. Because packet loss is rare or even non-existent in typical campus networks, the server in this lab injects artificial loss to simulate the effects of network packet loss. The server creates a variable randomized integer which determines whether a particular incoming packet is lost or not.

In the sample code, 30% of the client’s packets are simulated to be lost. You should study this sample code carefully, as it will help you write your Ping client. The server sits in an infinite loop listening for incoming UDP packets. When a packet comes in and if a randomized integer is greater than or equal to 4, the server simply <strong>capitalizes the encapsulated data and sends it back to the client</strong>; if the randomized integer is smaller than 3, the server needs to <strong>inform to the client which packet has been dropped</strong> and then <strong>client needs to retransmit the dropped packet</strong>.

<h1>Client Code</h1>

You need to develop your client code from scratch.

<h2>Ping Message Format</h2>

The ping messages in this lab are formatted in a simple way. The client message is one line, consisting of ASCII characters in the following format:

ping &lt;ping_index&gt; time_stamp

where ping_index starts at 1 and progresses to 100 for each successive ping message sent by the client, and time_stamp is the time when the client sends the message.

<h2>Functionalities of your client</h2>

You client program should support the following:

The client should send 100 pings to the server. Because UDP is an unreliable protocol, a packet sent from the client to the server may be lost in the network, or vice versa. Therefore, your client should <strong>support retransmitting the dropped packets</strong>. <strong>(Note that you client is not allowed to use socket timeout)</strong>

Specifically, your client program should

<ol>

 <li>send the <strong>ping message</strong> using UDP to the Ping server ;</li>

 <li>print the <strong>ping response message</strong> from the Ping server if the ping message has not been dropped ;</li>

 <li>retransmit the same ping message if the previous ping message(s) have been dropped by the Ping server ; print which ping message needs to be retransmitted ;</li>

 <li>calculate and print the round trip time (RTT) in seconds of each ping message/response pair. (Note that for the retransmitted ping request/response pairs, the starting time-stamp can be either the time-stamp of the <strong>initial</strong> ping request message or the <strong>most recent</strong> ping request message)</li>

</ol>

<h1>Run the code</h1>

<ol>

 <li>Start CSC361-VM , open a terminal, and type sudo mn -x to generate a simple network topology ;</li>

 <li>Flush all arp caches (more details can be found in the provided <strong>Wireshark<em>Ethernet</em>pdf</strong>) ;</li>

 <li>Run your Ping server over one of the hosts created (e.g., h1)</li>

</ol>

python pingserver.py &lt;IP addr of Ping server&gt; &lt;Port number of Ping server&gt;

<ol start="4">

 <li>Run your Ping client over one of the hosts created (e.g. h2)</li>

</ol>

python pingclient.py &lt;IP addr of Ping server&gt; &lt;Port number of Ping server&gt;