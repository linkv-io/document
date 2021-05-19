# The Advantages

# Industry-leading Core Functions

* Compared with the leading cloud service providers in China, the overall quality of the IM system is ahead of the others. The shown diagram indicates the message arrival rate is about 20% higher than other competitors.

![img](https://dl.linkv.io/doc/en/android/im/images/chart1.png)

* The delays in sending messages from the major countries around the world are about 20% ahead of the other competitors:

![img](https://dl.linkv.io/doc/en/android/im/images/chart2.png)

* The connection success rate of joining the live broadcast room is ahead of the other competitors:

![img](https://dl.linkv.io/doc/en/android/im/images/chart3.png)

# Key Metrics of IM Service

The LinkV-IM system has completed the systematic test, and the overall processing quality is leading the industry. The core parameters are as follows:

| Test items             | Concurrency/sec     | Remarks                          |
| -------------------- | ------------ | ----------------------------- |
| Intelligent navigation Service         | 20092.73 QPS | QPS: Queries Per Second。 |
| Message transmission speed         | 18232.78 QPS |                               |
| Sever message transmission speed           | 21530.09 QPS |                               |
| The maximum online connection of single server     | 1 million     | Memory occupied by a single connection: 3.66K       |
| Stability test           | 2 hours        |                               |
| Maximum number of people online in a single live broadcast room | 300, 000 people      |                               |
| Maximum throughput of messages in the live broadcast room | 110000 QPS   |                               |

# Message Security

In order to avoid the messages being intercepted during the transmission, the message content is encrypted during the transmission of the message protocol by a method similar to the https encryption process:

1. After the connection is established successfully, the client negotiates with the server. The clients obtain a data encryption key for the current session, which is a 32-bit string, and the clients take the last 16 digits as the data encryption key. This negotiation process of data transmission is using the RSA algorithm;
2. Data transmission is encrypted by this data encryption key. In order to ensure the efficiency, the stream cipher of RC4 algorithm is used;
3. The clients use the data encryption key to encrypt the message content by using the RC4 algorithm;
4. The servers decrypt the messages and store the message according to the data encryption keys that attached to each channel. 
5. For the receivers of the message, take out the data encryption keys of the current sessions, then re-encrypt the message, and push the message .

# International Deployment

At present, IM can deploy multiple data centers around the world according to user needs, or use AWS to achieve multi-regions and multi-data centers. The schematic diagram of multiple data centers shown as follows:

![img](https://dl.linkv.io/doc/en/android/im/images/aws.png)

#  
