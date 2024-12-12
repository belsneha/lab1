# lab1
TCL Program:  
lab1.tcl 
set ns [new Simulator]  
set nf [open lab1.nam w]  
$ns namtrace-all $nf  
set tf [open lab1.tr w]  
$ns trace-all $tf  
proc finish { } {  
global ns nf tf  
$ns flush-trace  
close $nf  
close $tf  
exec nam lab1.nam &  
exit 0  
} 
set n0 [$ns node]   
set n1 [$ns node]  
set n2 [$ns node]  
set n3 [$ns node]  
$ns duplex-link $n0 $n2 200Mb 10ms DropTail  
$ns duplex-link $n1 $n2 100Mb 5ms DropTail  
$ns duplex-link $n2 $n3 1Mb 1000ms DropTail  
$ns queue-limit $n0 $n2 10  
$ns queue-limit $n1 $n2 10 
set udp0 [new Agent/UDP]   
$ns attach-agent $n0 $udp0  
set cbr0 [new Application/Traffic/CBR]  
$cbr0 set packetSize_ 500  
$cbr0 set interval_ 0.005  
$cbr0 attach-agent $udp0  
set udp1 [new Agent/UDP]  
$ns attach-agent $n1 $udp1 
set cbr1 [new Application/Traffic/CBR]  
$cbr1 attach-agent $udp1 
set udp2 [new Agent/UDP]  
$ns attach-agent $n2 $udp2  
set cbr2 [new Application/Traffic/CBR]  
$cbr2 attach-agent $udp2  
set null0 [new Agent/Null]  
$ns attach-agent $n3 $null0  
$ns connect $udp0 $null0  
$ns connect $udp1 $null0  
$ns at 0.1 "$cbr0 start"  
$ns at 0.2 "$cbr1 start"  
$ns at 1.0 "finish"  
$ns run


AWK Program:  
lab1.awk 
BEGIN {  c=0;  
}  
{  
If ($1= ="d")  
{  
c++;  
printf("%s\t%s\n",$5,$11);  
}  
}  
END{  
printf("The number of packets dropped =%d\n",c);  
}



# lab2


TCL Program:  
lab2.tcl 
set ns [ new Simulator ] 
set nf [ open lab2.nam w ] 
$ns namtrace-all $nf 
set tf [ open lab2.tr w ] 
$ns trace-all $tf 
set n0 [$ns node] 
set n1 [$ns node] 
set n2 [$ns node] 
set n3 [$ns node] 
set n4 [$ns node] 
set n5 [$ns node] 
$n4 shape box 
$ns duplex-link $n0 $n4 1005Mb 1ms DropTail 
$ns duplex-link $n1 $n4 50Mb 1ms DropTail 
$ns duplex-link $n2 $n4 2000Mb 1ms DropTail 
$ns duplex-link $n3 $n4 200Mb 1ms DropTail 
$ns duplex-link $n4 $n5 1Mb 1ms DropTail 
set p1 [new Agent/Ping] 
$ns attach-agent $n0 $p1 
$p1 set packetSize_ 50000 
$p1 set interval_ 0.0001 
set p2 [new Agent/Ping] 
$ns attach-agent $n1 $p2
set p3 [new Agent/Ping] 
$ns attach-agent $n2 $p3 
$p3 set packetSize_30000 
$p3 set interval_ 0.00001 
set p4 [new Agent/Ping] 
$ns attach-agent $n3 $p4 
set p5 [new Agent/Ping] 
$ns attach-agent $n5 $p5 
$ns queue-limit $n0 $n4 5 
$ns queue-limit $n2 $n4 3b 
$ns queue-limit $n4 $n5 2 
Agent/Ping instproc recv {from rtt} { 
$self instvar node_ 
puts "node [$node_ id] received answer from $from with round trip time $rtt msec" 
} 
$ns connect $p1 $p5 
$ns connect $p3 $p4 
proc finish { } { 
global ns nf tf 
$ns flush-trace 
close $nf 
close $tf 
exec nam lab2.nam & 
exit 0 
}
$ns at 0.1 "$p1 send" 
$ns at 0.2 "$p1 send" 
$ns at 0.3 "$p1 send" 
$ns at 0.4 "$p1 send" 
$ns at 0.5 "$p1 send" 
$ns at 0.6 "$p1 send" 
$ns at 0.7 "$p1 send" 
$ns at 0.8 "$p1 send" 
$ns at 0.9 "$p1 send" 
$ns at 1.0 "$p1 send" 
$ns at 1.1 "$p1 send" 
$ns at 1.2 "$p1 send" 
$ns at 1.3 "$p1 send" 
$ns at 1.4 "$p1 send" 
$ns at 1.5 "$p1 send" 
$ns at 1.6 "$p1 send" 
$ns at 1.7 "$p1 send" 
$ns at 1.8 "$p1 send" 
$ns at 1.9 "$p1 send" 
$ns at 2.0 "$p1 send" 
$ns at 2.1 "$p1 send" 
$ns at 2.2 "$p1 send" 
$ns at 2.3 "$p1 send" 
$ns at 2.4 "$p1 send" 
$ns at 2.5 "$p1 send" 
$ns at 2.6 "$p1 send" 
$ns at 2.7 "$p1 send" 
$ns at 2.8 "$p1 send" 
$ns at 2.9 "$p1 send" 
$ns at 0.1 "$p3 send" 
$ns at 0.2 "$p3 send"
$ns at 0.3 "$p3 send" 
$ns at 0.4 "$p3 send" 
$ns at 0.5 "$p3 send" 
$ns at 0.6 "$p3 send" 
$ns at 0.7 "$p3 send" 
$ns at 0.8 "$p3 send" 
$ns at 0.9 "$p3 send" 
$ns at 1.0 "$p3 send" 
$ns at 1.1 "$p3 send" 
$ns at 1.2 "$p3 send" 
$ns at 1.3 "$p3 send" 
$ns at 1.4 "$p3 send" 
$ns at 1.5 "$p3 send" 
$ns at 1.6 "$p3 send" 
$ns at 1.7 "$p3 send" 
$ns at 1.8 "$p3 send" 
$ns at 1.9 "$p3 send" 
$ns at 2.0 "$p3 send" 
$ns at 2.1 "$p3 send" 
$ns at 2.2 "$p3 send" 
$ns at 2.3 "$p3 send" 
$ns at 2.4 "$p3 send" 
$ns at 2.5 "$p3 send" 
$ns at 2.6 "$p3 send" 
$ns at 2.7 "$p3 send" 
$ns at 2.8 "$p3 send" 
$ns at 2.9 "$p3 send" 
$ns at 3.0 "finish" 
$ns run


AWK Program:  
lab2.awk 
BEGIN{ 
drop=0; 
} 
{ 
if($1=="d" ) 
{ 
drop++; 

} 
} END{ 
printf("Total number of %s packets dropped due to congestion =%d\n",$5,drop); 
} 



# lab4

Source code: 
import java.util.*; 
public class CRC  
{ 
 void div(int a[],int k) 
 { 
  int gp[]={1,0,0,0,1,0,0,0,0,0,0,1,0,0,0,0,1}; 
  int count=0; 
  for(int i=0;i<k;i++) 
  { 
   if(a[i]==gp[0]) 
   { 
    for(int j=i;j<17+i;j++) 
    { 
     a[j]=a[j]^gp[count++]; 
    } 
    count=0; 
   } 
  } 
 } 
 
 public static void main(String[] args) 
 { 
  int a[]=new int[100]; 
  int b[]=new int[100]; 
  int len,k; 
  CRC ob=new CRC(); 
  System.out.println("Enter the length of Data Frame:"); 
  Scanner sc=new Scanner(System.in); 
len=sc.nextInt(); 
  int flag=0; 
  System.out.println("Enter the Message:"); 
  for(int i=0;i<len;i++) 
  {  
   a[i]=sc.nextInt(); 
  } 
  for(int i=0;i<16;i++) 
  {  
   a[len++]=0; 
  } 
  k=len-16; 
  for(int i=0;i<len;i++) 
  {  
   b[i]=a[i]; 
  } 
  ob.div(a,k); 
  for(int i=0;i<len;i++) 
  a[i]=a[i]^b[i]; 
  System.out.println("Data to be transmitted: "); 
  for(int i=0;i<len;i++) 
  { 
   System.out.print(a[i]+" "); 
  } 
  System.out.println(); 
  System.out.println("Enter the Received Data: "); 
  for(int i=0;i<len;i++) 
  { 
   a[i]=sc.nextInt();
   } 
  ob.div(a, k); 
  for(int i=0;i<len;i++) 
  { 
   if(a[i]!=0) 
   { 
    flag=1; 
    break; 
   } 
  } 
  if(flag==1) 
   System.out.println("error in data"); 
  else 
   System.out.println("no error"); 
 } 
} 


# lab6

import java.util.Scanner; 
public class BellmanFord 
{ 
    private int d[]; 
    private int nov; 
    public static final int MAX_VALUE = 999; 
    public BellmanFord(int nov) 
    { 
        this.nov = nov; 
        d = new int[nov + 1]; 
    } 
    public void BellmanFordEvaluation(int s, int am[][]) 
    { 
        for (int n = 1; n <= nov; n++) 
        { 
            d[n] = MAX_VALUE; 
        } 
        d[s] = 0; 
        for (int n = 1; n <= nov - 1; n++) 
        { 
            for (int sn = 1; sn <= nov; sn++) 
            { 
                for (int dn = 1; dn <= nov; dn++)  
  {  
   if (am[sn][dn] != MAX_VALUE)  
   {  
    if (d[dn] > d[sn] + am[sn][dn]) 
                              d[dn] = d[sn] + am[sn][dn]; 
                 } 
                } 
            } 
        } 
for (int sn = 1; sn <= nov; sn++) 
        { 
            for (int dn = 1; dn <= nov; dn++) 
     { 
   if (am[sn][dn] != MAX_VALUE)  
   {  
   if(d[dn] > d[sn] + am[sn][dn]) 
                          { 
    System.out.println("The Graph contains negative egde cycle"); 
    break; 
   } 
                } 
            } 
        }   
        for (int v = 1; v <= nov; v++) 
        { 
            System.out.println("Distance of source  " + s + " to " + v + " is " + d[v]); 
        } 
    } 
    public static void main(String args[]) 
    { 
        int nov = 0; 
        int s; 
        Scanner scanner = new Scanner(System.in); 
        System.out.println("Enter the number of vertices"); 
        nov = scanner.nextInt(); 
        int am[][] = new int[nov + 1][nov + 1]; 
        System.out.println("Enter the adjacency matrix"); 
        for (int sn = 1; sn <= nov; sn++) 
        { 
            for (int dn = 1; dn <= nov; dn++) 
            { 
                am[sn][dn] = scanner.nextInt(); 
if (sn == dn) 
{ 
am[sn][dn] = 0; 
continue; 
} 
if (am[sn][dn] == 0) 
{ 
am[sn][dn] = MAX_VALUE; 
} 
} 
} 
System.out.println("Enter the source vertex"); 
s = scanner.nextInt(); 
BellmanFord bellmanford = new BellmanFord(nov); 
bellmanford.BellmanFordEvaluation(s, am); 
scanner.close();  
} 
}


# lab8

 
UDPServer.java 
import java.net.*; 
public class UDPServer 
{ 
 public static void main(String[] args) 
 { 
  DatagramSocket skt=null; 
  try 
  { 
   skt=new DatagramSocket(6788);  
   byte[] buffer = new byte[1000]; 
   System.out.println("Listening on port 6788"); 
   while(true) 
   { 
    DatagramPacket request = new DatagramPacket(buffer,buffer.length); 
    skt.receive(request); 
    String message = new String(request.getData());  
    System.out.println("server received request "); 
    String toUpper = message.toUpperCase(); 
    byte[] sendMsg= toUpper.getBytes();  
    System.out.println("server sending response "); 
    DatagramPacket reply = new DatagramPacket(sendMsg,sendMsg.length, 
    request.getAddress(),request.getPort()); 
    skt.send(reply); 
   } 
  } 
  catch(Exception ex)
  { 
  } 
 } 
} 
 
UDPClient.java 
 
import java.net.*; 
import java.util.Scanner; 
public class UDPClient 
{ 
 public static void main(String[] args) 
 { 
  DatagramSocket skt; 
  Scanner scan = new Scanner(System.in); 
  try 
  { 
   System.out.println("Enter Message:"); 
   String msg= scan.next();    
   skt=new DatagramSocket();  
 
   byte[] b = msg.getBytes(); 
   InetAddress host=InetAddress.getByName("127.0.0.1");  
   int serverPort=6788; 
   DatagramPacket request =new DatagramPacket (b,b.length,host,serverPort);  
   skt.send(request); 
   byte[] buffer =new byte[1000]; 
   DatagramPacket reply= new DatagramPacket(buffer,buffer.length);  
   skt.receive(reply);
   String s1 = new String(reply.getData()); 
   System.out.println("Client received: " + s1.trim());  
   skt.close(); 
  } 
  catch(Exception ex) 
  { 
  } 
 } 
} 


# lab10

import java.util.Scanner; 
public class LeakyBucket 
{ 
 public static void main(String args[]) 
 { 
  int n, outgoing, store, bucketSize; 
  int incoming[];  
  Scanner scan = new Scanner(System.in); 
  System.out.println("Enter number of inputs"); 
  n = scan.nextInt(); 
  incoming = new int[n]; 
  for(int i = 0 ;i< n ; i++) 
  { 
   System.out.println("Enter incoming packet size "+(i+1)); 
   incoming[i] = scan.nextInt();  
  }  
  System.out.println("Enter bucket size"); 
  bucketSize = scan.nextInt(); 
  System.out.println("Enter outgoing rate"); 
  outgoing = scan.nextInt(); 
  store = 0; 
  int i = 0; 
  System.out.println("Packet Recieved | Packet Dropped | Packet Sent | Packet Left"); 
 
  do 
  {
  int pktReceived = 0, pktSent = 0,pktDrop = 0; 
   if(i < n) 
   { 
    pktReceived = incoming[i]; 
    if(pktReceived  <= (bucketSize - store)) 
    { 
     store += pktReceived ; 
    } 
    else 
    { 
     pktDrop = pktReceived -(bucketSize - store); 
     store = bucketSize; 
    } 
   } 
   if(store > outgoing)  
   { 
    store -= outgoing; 
    pktSent = outgoing; 
   } 
   else 
   { 
    pktSent = store; 
    store = 0; 
   } 
   System.out.println(pktReceived +"\t\t"+pktDrop+"\t\t"+pktSent+"\t\t"+store); 
   try
   { 
    Thread.sleep(2000); 
   } 
   catch(Exception e) 
   { 
   } 
   i++; 
    
  }while(store != 0 || i < n);  
 
 } 
}







