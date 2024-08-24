  # Capstone Project : AIML Approach for Securing 4G/5G Applications- Melicious Attack Classification
  ### By Mohammad Abu-Samra

[Link to notebook:] Capstone_part1.ipynb at main · https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/capstone_part1.ipynb) 



## Context

The goal of this project is to define an inteligent self-adaptive mechanism for securing 4G/5G cellular networks which detects/prevents attacks launched by cellular devices. The mechanism includes data exploration and quality check of the network generated data and select the best model based on the performance of the classifiers (k-nearest neighbors, logistic regression, decision trees, and support vector machines). The dataset used is related to network intrusion detection generatde over 5G wireless network and comes from [kaggle](https://www.kaggle.com/datasets/humera11/5g-nidd-dataset). 



# 1 Business Understanding



## 1.1 Background



With the large number of new connections, features, and services introduced, the 4th and 5th wireless generations (4G/5G) technologies reflect the development of mobile communication networks and is here to stay for the next decade. The multitude of services and technologies that LTE/5G incorporate have made modern com- munication networks very complex and sophisticated in nature. This complexity along with the incorporation of Machine Learning (ML) and Artificial Intelligence (AI) provides the opportunity for the attackers to launch intelligent attacks against the network and network devices. These attacks often traverse undetected due to the lack of intelligent security mechanisms to counter these threats. 

Therefore, the implementation of real-time, proactive, and self-adaptive security mechanisms throughout the network would be an integral part of 4G/5G as well as future communication systems. Large amounts of data collected from real networks will play an important role in the training of AI/ML models to identify and detect malicious content in network traffic. This work presents 5G Network Intrusion Detection Dataset (5G-NIDD), a fully labeled dataset built on a functional 5G test network that can be used by those who develop and test AI/ML solutions. The work further analyses the collected data using common ML models and shows the achieved accuracy levels.  Although the dataset was collected from running test traffic on 5G networ it still can be used for 4G/LTE as well.

The following approach will be taken as part of implementing the self-adaptive security mechanism:

- Binary classification - identify cellular device originated messages as 'benign' or 'melicious' taking the binary classification approach 
- Multi-Class classification - identify melicious message 'attack type' taking the multi-class classification approach using one-versus-one strategy

The Binary classification allows the system to detect a threat while the multi-class classification allows the system to take specific steps to neutralize the threat.



## 1.2 Business Goals and KPI

The business objective is to find the best models to identify and detect malicious content in network traffic. This model will help cellular service providers providing secure and reliable applications to thier customers, improving business outcomes.



# 2 Data Understanding

This section provides information about the data, its description and is its exploration to make sure it fits the business goals.



## 2.1 **Gathering and Describing Data**

This data comes from [UCI Machine Learning repository Links to an external site.](https://archive.ics.uci.edu/ml/datasets/bank+marketing). 



Here is a sample of the data:



 |  `Unnamed: 0`  |     `Seq`  |  `Dur`  |   `RunTime`  |      `Mean`  |       `Sum`  |       `Min`  |       `Max`  |     `Proto`  |  `sTos`  |   `dTos`  |   `sDSb`  |  `dDSb`  |  `sTtl`  |   `dTtl`  |  `sHops`  |  `dHops`  |  `Cause`  |  `TotPkts`  |  `SrcPkts`  |  `DstPkts`  |  `TotBytes`  |  `SrcBytes`  |  `DstBytes`  |  `Offset`  |  `sMeanPktSz`  |  `dMeanPktSz`  |        `Load`  |       `SrcLoad`  |      `DstLoad`  |          `Loss`  |  `SrcLoss`  |  `DstLoss`  |  `pLoss`  |  `SrcGap`  |  `DstGap`  |  `Rate`  |    `SrcRate`  |    `DstRate`  |     `State`  |  `SrcWin`  |  `DstWin`  |   `sVid`  |   `dVid`  |  `SrcTCPBase`  |    `DstTCPBase`  |        `TcpRtt`  |  `SynAck`  |  `AckDat`  |  `Label`  |  `Attack Type`  |  `Attack Tool`  |            | 
 |  -----------:  |  -------:  |  ----:  |  ---------:  |  ---------:  |  ---------:  |  ---------:  |  ---------:  |  ---------:  |  -----:  |  ------:  |  ------:  |  -----:  |  -----:  |  ------:  |  ------:  |  ------:  |  ------:  |  --------:  |  --------:  |  --------:  |  ---------:  |  ---------:  |  ---------:  |  -------:  |  -----------:  |  -----------:  |  -----------:  |  -------------:  |  ------------:  |  -------------:  |  --------:  |  --------:  |  ------:  |  -------:  |  -------:  |  -----:  |  ----------:  |  ----------:  |  ---------:  |  -------:  |  -------:  |  ------:  |  ------:  |  -----------:  |  -------------:  |  -------------:  |  -------:  |  -------:  |  ------:  |  ------------:  |  ------------:  |  --------  | 
 |     `1215885`  |  `487569`  |    `1`  |  `0.000000`  |  `0.000000`  |  `0.000000`  |  `0.000000`  |  `0.000000`  |  `0.000000`  |  `sctp`  |  `186.0`  |  `186.0`  |    `ef`  |    `ef`  |  `252.0`  |  `255.0`  |    `4.0`  |    `1.0`  |   `Status`  |        `2`  |        `1`  |         `1`  |       `200`  |       `102`  |      `98`  |      `190300`  |  `102.000000`  |   `98.000000`  |      `0.000000`  |     `0.000000`  |      `0.000000`  |        `0`  |        `0`  |      `0`  |     `0.0`  |     `NaN`  |   `NaN`  |   `0.000000`  |   `0.000000`  |  `0.000000`  |     `CON`  |     `NaN`  |    `NaN`  |  `610.0`  |         `NaN`  |           `NaN`  |           `NaN`  |     `0.0`  |     `0.0`  |    `0.0`  |       `Benign`  |       `Benign`  |  `Benign`  | 
 |     `1215886`  |  `487570`  |    `3`  |  `0.235607`  |  `0.235607`  |  `0.235607`  |  `0.235607`  |  `0.235607`  |  `0.235607`  |  `sctp`  |  `186.0`  |   `40.0`  |    `ef`  |  `af11`  |  `255.0`  |  `250.0`  |    `1.0`  |    `6.0`  |   `Status`  |        `6`  |        `3`  |         `3`  |      `3056`  |       `290`  |    `2766`  |      `190392`  |   `96.666664`  |  `922.000000`  |  `69199.984380`  |  `6587.240723`  |  `62612.742190`  |        `0`  |        `0`  |      `0`  |     `0.0`  |     `NaN`  |   `NaN`  |  `21.221781`  |   `8.488712`  |  `8.488712`  |     `CON`  |     `NaN`  |    `NaN`  |    `NaN`  |       `610.0`  |           `NaN`  |           `NaN`  |     `0.0`  |     `0.0`  |    `0.0`  |       `Benign`  |       `Benign`  |  `Benign`  | 
 |     `1215887`  |  `487571`  |  `764`  |  `0.099927`  |  `0.099927`  |  `0.099927`  |  `0.099927`  |  `0.099927`  |  `0.099927`  |   `tcp`  |    `0.0`  |    `0.0`  |   `cs0`  |   `cs0`  |   `64.0`  |  `114.0`  |    `0.0`  |   `14.0`  |    `Start`  |        `3`  |        `2`  |         `1`  |       `252`  |       `160`  |      `92`  |      `190496`  |   `80.000000`  |   `92.000000`  |   `6404.675293`  |  `6404.675293`  |      `0.000000`  |        `0`  |        `0`  |      `0`  |     `0.0`  |     `0.0`  |   `0.0`  |  `20.014610`  |  `10.007305`  |  `0.000000`  |     `CON`  |   `213.0`  |  `273.0`  |    `NaN`  |         `NaN`  |  `2.237373e+09`  |  `1.983280e+09`  |     `0.0`  |     `0.0`  |    `0.0`  |       `Benign`  |       `Benign`  |  `Benign`  | 
 |     `1215888`  |  `487572`  |    `3`  |  `1.307852`  |  `1.307852`  |  `1.307852`  |  `1.307852`  |  `1.307852`  |  `1.307852`  |  `sctp`  |  `186.0`  |   `40.0`  |    `ef`  |  `af11`  |  `255.0`  |  `250.0`  |    `1.0`  |    `6.0`  |   `Status`  |        `6`  |        `3`  |         `3`  |       `596`  |       `306`  |     `290`  |      `190704`  |  `102.000000`  |   `96.666664`  |   `2434.526123`  |  `1247.847534`  |   `1186.678589`  |        `0`  |        `0`  |      `0`  |     `0.0`  |     `NaN`  |   `NaN`  |   `3.823062`  |   `1.529225`  |  `1.529225`  |     `CON`  |     `NaN`  |    `NaN`  |    `NaN`  |       `610.0`  |           `NaN`  |           `NaN`  |     `0.0`  |     `0.0`  |    `0.0`  |       `Benign`  |       `Benign`  |  `Benign`  | 
 |     `1215889`  |  `487573`  |    `1`  |  `0.476803`  |  `0.476803`  |  `0.476803`  |  `0.476803`  |  `0.476803`  |  `0.476803`  |  `sctp`  |  `186.0`  |  `186.0`  |    `ef`  |    `ef`  |  `252.0`  |  `255.0`  |    `4.0`  |    `1.0`  |   `Status`  |        `4`  |        `2`  |         `2`  |       `392`  |       `200`  |     `192`  |      `190808`  |  `100.000000`  |   `96.000000`  |   `3288.569824`  |  `1677.841797`  |   `1610.728149`  |        `0`  |        `0`  |      `0`  |     `0.0`  |     `NaN`  |   `NaN`  |   `6.291907`  |   `2.097302`  |  `2.097302`  |     `CON`  |     `NaN`  |    `NaN`  |  `610.0`  |         `NaN`  |           `NaN`  |           `NaN`  |     `0.0`  |     `0.0`  |    `0.0`  |       `Benign`  |       `Benign`  |  `Benign`  | 



Following features of the provided sample data above:

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1215890 entries, 0 to 1215889
Data columns (total 52 columns):
 #   Column       Non-Null Count    Dtype  
---  ------       --------------    -----  
 0   Unnamed: 0   1215890 non-null  int64  
 1   Seq          1215890 non-null  int64  
 2   Dur          1215890 non-null  float64
 3   RunTime      1215890 non-null  float64
 4   Mean         1215890 non-null  float64
 5   Sum          1215890 non-null  float64
 6   Min          1215890 non-null  float64
 7   Max          1215890 non-null  float64
 8   Proto        1215890 non-null  object 
 9   sTos         1215676 non-null  float64
 10  dTos         272823 non-null   float64
 11  sDSb         1215676 non-null  object 
 12  dDSb         272823 non-null   object 
 13  sTtl         1215676 non-null  float64
 14  dTtl         272823 non-null   float64
 15  sHops        1215676 non-null  float64
 16  dHops        272823 non-null   float64
 17  Cause        1215890 non-null  object 
 18  TotPkts      1215890 non-null  int64  
 19  SrcPkts      1215890 non-null  int64  
 20  DstPkts      1215890 non-null  int64  
 21  TotBytes     1215890 non-null  int64  
 22  SrcBytes     1215890 non-null  int64  
 23  DstBytes     1215890 non-null  int64  
 24  Offset       1215890 non-null  int64  
 25  sMeanPktSz   1215890 non-null  float64
 26  dMeanPktSz   1215890 non-null  float64
 27  Load         1215890 non-null  float64
 28  SrcLoad      1215890 non-null  float64
 29  DstLoad      1215890 non-null  float64
 30  Loss         1215890 non-null  int64  
 31  SrcLoss      1215890 non-null  int64  
 32  DstLoss      1215890 non-null  int64  
 33  pLoss        1215890 non-null  float64
 34  SrcGap       278671 non-null   float64
 35  DstGap       278671 non-null   float64
 36  Rate         1215890 non-null  float64
 37  SrcRate      1215890 non-null  float64
 38  DstRate      1215890 non-null  float64
 39  State        1215890 non-null  object 
 40  SrcWin       242420 non-null   float64
 41  DstWin       177078 non-null   float64
 42  sVid         114571 non-null   float64
 43  dVid         2009 non-null     float64
 44  SrcTCPBase   278671 non-null   float64
 45  DstTCPBase   230047 non-null   float64
 46  TcpRtt       1215890 non-null  float64
 47  SynAck       1215890 non-null  float64
 48  AckDat       1215890 non-null  float64
 49  Label        1215890 non-null  object 
 50  Attack Type  1215890 non-null  object 
 51  Attack Tool  1215890 non-null  object 
dtypes: float64(32), int64(12), object(8)
memory usage: 482.4+ MB
```



The description of the data is as follows:

Understanding the Features

Data description:

```
Input variables:

1 - Seq (numeric) - argus sequence number.
2 - Dur (numeric) - record total duration. 
3 - RunTime (numeric) - total active flow run time. This value is generated through aggregation, and is the sum
of the records duration.
4 - Mean (numeric) - average duration of aggregated records.
5 - Sum (numeric) - total accumulated durations of aggregated records.
6 - Min (numeric) - minimum duration of aggregated records.
7 - Max (numeric) - maximum duration of aggregated records.
8 - Proto (Categorical) - transaction protocol.
9 - sTos (numeric) - source TOS byte value.
10 - dTos (numeric) - destination TOS byte value.
11 - sDSb (categorical) - source diff serve byte value.
12 - dDSb (categorical) - destination diff serve byte value.
13 - sTtl (numeric) - src -> dst TTL value.
14 - dTtl (numeric) - dst -> src TTL value.
15 - sHops (numeric) - estimate of number of IP hops from src to this point.
16 - dHops (numeric) - estimate of number of IP hops from dst to this point.
17 - Cause (categorical) - Argus record cause code. Valid values are Start, Status, Stop, Close, Error.
18 - TotPkts (numeric) - total transaction packet count.
19 - SrcPkts (numeric) - src -> dst packet count.
20 - DstPkts (numeric) - dst -> src packet count.
21 - TotBytes (numeric) - total transaction bytes.
22 - SrcBytes (numeric) - src -> dst transaction bytes.
23 - DstBytes (numeric) - dst -> src transaction bytes.
24 - Offset (numeric) - record byte offset in file or stream.
25 - sMeanPktSz (numeric) - Mean of the flow packet size transmitted by the src (initiator).
26 - dMeanPktSz (numeric) - Mean of the flow packet size transmitted by the dst (target).
27 - Load (numeric) - bits per second.
28 - SrcLoad (numeric) - source bits per second.
29 - DstLoad (numeric) - destination bits per second.
30 - Loss (numeric) - pkts retransmitted or dropped.
31 - SrcLoss (numeric) - source pkts retransmitted or dropped.
32 - DstLoss (numeric) - destination pkts retransmitted or dropped.
33 - pLoss (numeric) - percent pkts retransmitted or dropped.
34 - SrcGap (numeric) - source bytes missing in the data stream.
35 - DstGap (numeric) - destination bytes missing in the data stream.
36 - Rate (numeric) - pkts per second.
37 - SrcRate (numeric) - source pkts per second.
38 - DstRate (numeric) - destination pkts per second.
39 - State (categorical) - transaction state.
40 - SrcWin (numeric) - source TCP window advertisement.
42 - DstWin (numeric) - destination TCP window advertisement.
43 - sVid (numeric) - source VLAN identifier.
44 - dVid (numeric) - destination VLAN identifier.
45 - SrcTCPBase (numeric) - source TCP base sequence number.
46 - DstTCPBase (numeric) - destination TCP base sequence number.
47 - TcpRtt (numeric) - TCP connection setup round-trip time, the sum of ’synack’ and ’ackdat’.
48 - SynAck (numeric) - TCP connection setup time, the time between the SYN and the SYN_ACK packets.
49 - AckDat (numeric) - TCP connection setup time, the time between the SYN_ACK and the ACK packets.
50 - Attack Tool (categorical) - Type of source that launched the attack.

Target Labels:
51 - Label (categorical) - Benign or Melicious.
52 - Attack Type (categorical) - Type of attack.
```





A sample set of size 50K was randomly selected to represent the 1.2M entries, because of the cost of processing 1.2M entries in terms of high CPU processing power and more importantly the time it takes (3+ weeks) to evaluate and select the suitable model.



Upon closely examining the data, following features were removed since they were not relevent to 'Y' (i.e., they were intriduced by Argus tool as part of message flow generation) :

- Unnamed, Seq, Cause, and Attack Tool.

  Note: the index was reset.



Here is want the samlple data of the randomly selected 50K entires post removal of features not related to 'Y':

```
Index: 50000 entries, 875284 to 1015284
Data columns (total 52 columns):
 #   Column       Non-Null Count  Dtype  
---  ------       --------------  -----  
 0   Unnamed: 0   50000 non-null  int64  
 1   Seq          50000 non-null  int64  
 2   Dur          50000 non-null  float64
 3   RunTime      50000 non-null  float64
 4   Mean         50000 non-null  float64
 5   Sum          50000 non-null  float64
 6   Min          50000 non-null  float64
 7   Max          50000 non-null  float64
 8   Proto        50000 non-null  object 
 9   sTos         49992 non-null  float64
 10  dTos         10967 non-null  float64
 11  sDSb         49992 non-null  object 
 12  dDSb         10967 non-null  object 
 13  sTtl         49992 non-null  float64
 14  dTtl         10967 non-null  float64
 15  sHops        49992 non-null  float64
 16  dHops        10967 non-null  float64
 17  Cause        50000 non-null  object 
 18  TotPkts      50000 non-null  int64  
 19  SrcPkts      50000 non-null  int64  
 20  DstPkts      50000 non-null  int64  
 21  TotBytes     50000 non-null  int64  
 22  SrcBytes     50000 non-null  int64  
 23  DstBytes     50000 non-null  int64  
 24  Offset       50000 non-null  int64  
 25  sMeanPktSz   50000 non-null  float64
 26  dMeanPktSz   50000 non-null  float64
 27  Load         50000 non-null  float64
 28  SrcLoad      50000 non-null  float64
 29  DstLoad      50000 non-null  float64
 30  Loss         50000 non-null  int64  
 31  SrcLoss      50000 non-null  int64  
 32  DstLoss      50000 non-null  int64  
 33  pLoss        50000 non-null  float64
 34  SrcGap       11434 non-null  float64
 35  DstGap       11434 non-null  float64
 36  Rate         50000 non-null  float64
 37  SrcRate      50000 non-null  float64
 38  DstRate      50000 non-null  float64
 39  State        50000 non-null  object 
 40  SrcWin       9991 non-null   float64
 41  DstWin       7149 non-null   float64
 42  sVid         4662 non-null   float64
 43  dVid         84 non-null     float64
 44  SrcTCPBase   11434 non-null  float64
 45  DstTCPBase   9287 non-null   float64
 46  TcpRtt       50000 non-null  float64
 47  SynAck       50000 non-null  float64
 48  AckDat       50000 non-null  float64
 49  Label        50000 non-null  object 
 50  Attack Type  50000 non-null  object 
 51  Attack Tool  50000 non-null  object 
dtypes: float64(32), int64(12), object(8)
memory usage: 20.2+ MB
```

```
              index           Dur       RunTime          Mean           Sum  \
count  5.000000e+04  50000.000000  50000.000000  50000.000000  50000.000000   
mean   6.057649e+05      1.365648      1.365648      1.365648      1.365648   
std    3.519909e+05      1.695812      1.695812      1.695812      1.695812   
min    9.900000e+01      0.000000      0.000000      0.000000      0.000000   
25%    3.002335e+05      0.000000      0.000000      0.000000      0.000000   
50%    6.047545e+05      0.000000      0.000000      0.000000      0.000000   
75%    9.120490e+05      2.580601      2.580601      2.580601      2.580601   
max    1.215879e+06      5.978457      5.978457      5.978457      5.978457   

                Min           Max          sTos          dTos          sTtl  \
count  50000.000000  50000.000000  49992.000000  10967.000000  49992.000000   
mean       1.365648      1.365648      0.887862      2.920580     81.264502   
std        1.695812      1.695812     12.645925     22.213269     55.753767   
min        0.000000      0.000000      0.000000      0.000000     36.000000   
25%        0.000000      0.000000      0.000000      0.000000     63.000000   
50%        0.000000      0.000000      0.000000      0.000000     63.000000   
75%        2.580601      2.580601      0.000000      0.000000     63.000000   
max        5.978457      5.978457    224.000000    186.000000    255.000000   

               dTtl         sHops         dHops       TotPkts       SrcPkts  \
count  10967.000000  49992.000000  10967.000000  50000.000000  50000.000000   
mean      65.675116      2.281665      5.035926      5.164080      3.690700   
std       29.208779      3.619798      2.283521     27.482485     18.548598   
min       37.000000      0.000000      0.000000      1.000000      0.000000   
25%       59.000000      1.000000      5.000000      1.000000      1.000000   
50%       59.000000      1.000000      5.000000      2.000000      1.000000   
75%       59.000000      1.000000      5.000000      2.000000      2.000000   
max      255.000000     28.000000     27.000000   2123.000000    646.000000   

            DstPkts      TotBytes       SrcBytes      DstBytes        Offset  \
count  50000.000000  5.000000e+04   50000.000000  5.000000e+04  5.000000e+04   
mean       1.473380  3.670563e+03    2498.207300  1.172355e+03  1.238446e+07   
std       15.739453  3.306756e+04   24331.163369  2.148973e+04  1.072870e+07   
min        0.000000  4.200000e+01       0.000000  0.000000e+00  2.320000e+02   
25%        0.000000  4.200000e+01      42.000000  0.000000e+00  2.993984e+06   
50%        0.000000  8.400000e+01      74.000000  0.000000e+00  9.918764e+06   
75%        0.000000  8.400000e+01      84.000000  0.000000e+00  1.909702e+07   
max     1938.000000  2.678814e+06  618604.000000  2.632269e+06  3.968934e+07   

        sMeanPktSz    dMeanPktSz          Load       SrcLoad       DstLoad  \
count  50000.00000  50000.000000  5.000000e+04  5.000000e+04  5.000000e+04   
mean      72.94686     59.602163  2.306560e+06  8.215287e+04  2.224407e+06   
std      142.92781    210.736530  3.894396e+08  9.929236e+06  3.798591e+08   
min        0.00000      0.000000  0.000000e+00  0.000000e+00  0.000000e+00   
25%       42.00000      0.000000  0.000000e+00  0.000000e+00  0.000000e+00   
50%       42.00000      0.000000  0.000000e+00  0.000000e+00  0.000000e+00   
75%       67.00000      0.000000  1.304976e+02  1.304825e+02  0.000000e+00   
max     1467.00000   1465.310303  8.619200e+10  2.112000e+09  8.408000e+10   

               Loss       SrcLoss      DstLoss        pLoss   SrcGap  \
count  50000.000000  50000.000000  50000.00000  50000.00000  11434.0   
mean       0.023220      0.013440      0.00978      0.34154      0.0   
std        0.263595      0.183576      0.15964      3.62841      0.0   
min        0.000000      0.000000      0.00000      0.00000      0.0   
25%        0.000000      0.000000      0.00000      0.00000      0.0   
50%        0.000000      0.000000      0.00000      0.00000      0.0   
75%        0.000000      0.000000      0.00000      0.00000      0.0   
max       18.000000      9.000000      9.00000     50.00000      0.0   

             DstGap          Rate       SrcRate       DstRate        SrcWin  \
count  11434.000000  5.000000e+04  5.000000e+04  5.000000e+04  9.991000e+03   
mean       0.837502  6.001478e+02  1.479761e+02  2.505720e+02  8.638408e+05   
std       52.744321  6.270245e+04  1.915159e+04  3.669199e+04  4.803209e+06   
min        0.000000  0.000000e+00  0.000000e+00  0.000000e+00  0.000000e+00   
25%        0.000000  0.000000e+00  0.000000e+00  0.000000e+00  5.657600e+04   
50%        0.000000  0.000000e+00  0.000000e+00  0.000000e+00  5.708800e+04   
75%        0.000000  3.885352e-01  3.883110e-01  0.000000e+00  6.425600e+04   
max     4104.000000  1.300000e+07  4.000000e+06  8.000000e+06  3.355392e+07   

             DstWin    sVid   dVid    SrcTCPBase    DstTCPBase        TcpRtt  \
count  7.149000e+03  4662.0   84.0  1.143400e+04  9.287000e+03  50000.000000   
mean   7.233932e+04   610.0  610.0  2.074003e+09  2.136603e+09      0.004538   
std    2.789521e+05     0.0    0.0  1.240331e+09  1.243652e+09      0.016702   
min    0.000000e+00   610.0  610.0  7.033740e+05  2.599570e+05      0.000000   
25%    6.476800e+04   610.0  610.0  1.008599e+09  1.062747e+09      0.000000   
50%    6.489600e+04   610.0  610.0  2.013988e+09  2.131052e+09      0.000000   
75%    6.502400e+04   610.0  610.0  3.140653e+09  3.225220e+09      0.000000   
max    1.677696e+07   610.0  610.0  4.294967e+09  4.294531e+09      1.051236   

             SynAck        AckDat  
count  50000.000000  50000.000000  
mean       0.000549      0.003988  
std        0.012181      0.010393  
min        0.000000      0.000000  
25%        0.000000      0.000000  
50%        0.000000      0.000000  
75%        0.000000      0.000000  
max        1.024679      0.231634 
```




***Here are some additional details on target columns - <u>'Label' and 'Attack Type'</u>:***

**1 - *DoS Attacks* Types -** A DoS attack is one of the most common attacks that can occur in a network. The aim of this attack is to slow down or completely shut down a target making it inaccessible to legitimate users. Flooding techniques and malicious content injection are some of the common methods to lunch a DoS attack. The network or a node will eventually undergo resource exhaustion and deny the nonmalicious users’ access as a result of a DoS attack. Due to the heterogeneous nature of the 5G networks, DoS attacks impose a vital threat in 5G which may target the network nodes, devices, and applications.

​ | **a) *Benign Traffic:*** The benign traffic profile includes protocols such as HTTP, HTTPS, SSH, and Secure File Transfer Protocol (SFTP). 

​ | **b) *ICMP Flood:*** Internet Control Message Protocol (ICMP) flood attacks use ICMP echo requests to flood a target at a very high frequency. Ideally, an ICMP echo reply follows the echo request to the same Internet Protocol (IP) address. In this type of attack, the target will send back echo replies to massive amounts of ICMP echo requests. The higher frequency of echo requests also leads to a higher frequency in the rate of response which eventually overwhelms the network and makes the services unavailable for normal users.

​ | **c) *UDP Flood:*** In a User Datagram Protocol (UDP) flood attack, attacker sends UDP packets at a higher rate. Since UDP is a connection-less protocol, it is possible to send a large amount of traffic. As the UDP packets arrive at the target destination, the reply is a “Destination Unreachable” packet if no associated application is found. Over time, as a higher amount of UDP packets are received and responded to, the system eventually becomes nonresponsive.

​ | **d) *SYN Flood:*** SYN flood attack is a result of the exploitation of the TCP three way handshake. In a typical TCP communication between two nodes, the source nodes sends a SYN packet to the desired node for the initiation of the connection. The destination node replies with a SYN ACK to acknowledge the SYN packet. Finally, the source sends another ACK to acknowledge receiving the SYN ACK, completing the three way handshake. In a SYN flood attack, the attacker does not perform the final step of the TCP handshake, therefore leaving the connection half open. The transmission of SYN packets at a higher frequency will leave large amounts of ports half open for a certain period and eventually the receiver will be exhausted once all ports are occupied preventing access for legitimate users.

​ | **e) *HTTP Flood:*** HTTP flood attacks target the application layer. It is a popular method for DoS/DDoS attacks due to its proven effectiveness in mimicking normal human behavior and thereby staying undetected. We used Python based Goldeneye tool to conduct the HTTP flood attacks. To perform the application layer attacks, we deployed a web server at the victim Multi-access Edge Computing (MEC) instance. The target was an Apache2 web server deployed in MEC.

​ | **f) *Slowrate DoS:*** Another exploitation of the application layer to conduct DoS attacks is the use of slow rate attacks. In terms of the speed and the number of packets directed at the target, it is comparatively different from other forms of DoS attacks. This slow nature of the traffic makes it harder to detect. In this exercise, we conducted two different forms of slow rate DoS attacks. As the first one, we performed slowloris attack through a python script. The attack establishes several connections with the targeted web server and maintain them for a longer period. We performed this by sending HTTP partial headers continuously to keep the connections open without completion. The web server waits for the connections to complete which might never occur. The opening of a large number of such connections will eventually lead to resource exhaustion. 

​ | In another case, the attacker sends slow POST requests to a web server. The POST requests comprises packets that specify a larger packet size in the header field, but the actual packet has a lesser size. The server then waits for the completion of the whole packet size specified in the header field.



**2 - *Port Scans*** - A port scan usually precedes an actual attack to identify opportunities for attacks via open ports. Typically, port scans send requests to a targeted range of ports in a targeted host and observe the response. The response is sufficient to determine the status of a specific port in most cases. In some instances, deeper knowledge such as the operating system of the target may also be discovered. Port scan is an efficient way to determine exploitable hosts in a network before the execution of attacks. The dataset contains attack data from different port scans such as the SYN scan, TCP Connect scan, and UDP scan.

​ | **a) *SYN Scan:*** The SYN scan uses part of the three way handshake in TCP connection establishment to discover open ports. The attacker sets the SYN flag in a TCP packet and sends to the target. If the targeted port/s is ready for a TCP connection, it returns a response packet with SYN and ACK flags set. This means the scan indicates an *open* port to the attacker. Ports that are not ready to establish a TCP connection send a RST packet indicating a *closed* port. As the attacker determines the state of the port from two packet flows, attacker cease the execution of the next step of the three way handshake. However, to terminate the connection the attacker may send an RST packet to the target once the information on the status of the port is collected. If not, the target will keep sending packets with SYN and ACK flags set until a response is seen from the attacker. Other than *open* or *closed* ports, a *filtered* port may imply that a firewall is blocking the packets or the host is not reachable.

​ | The incomplete three way handshake in SYN scan makes the scanning process quite fast in comparison to other available techniques. The SYN scan is one of the most popular scanning techniques.

​ | **b) *TCP Connect Scan:*** Similar to SYN scan, the TCP connect scan exploits the TCP handshake to perform the scanning process. However, the three way handshake is fully completed therefore, the time taken to scan the ports is higher compared with SYN Scan. Conversely, attackers may not need the same level of privileges to execute a TCP connect scan as they require for SYN scan.

​ | The execution of the TCP connect scan is similar to SYN scan with the addition of the completion step in the three way handshake. This means that the two initial packet flows (SYN flag set packet and SYN ACK flags set packet) take place for an *open* port. Subsequently, the target replies with a packet set with ACK flag to complete the three way handshake. Although the opening of a TCP connection also offers the potential for data exchange, the attacking operating system makes sure the connection is terminated as soon as it detects that one has been made. In the event of a *closed* port, target sends a RST packet to the host similar to the SYN scan. *Filtered* ports may also exist in this scenario.

​ | **c) *UDP Scan:*** UDP scan transmits UDP datagrams to the targeted ports of the targeted host. The attacker sends the UDP packets with a missing payload to ports that are not UDP. For UDP ports, a protocol-specific payload will exist. In UDP scan, the status of a port is defined based on the response of the target or the unresponsiveness of the target. As nonUDP ports receive a UDP datagram without a payload, the probability of getting a proper response is minimum. An *open | filtered* state is likely from such ports which indicates either a firewall is blocking the packets or packets are simply been forwarded from TCP/IP stack towards a listening application and discards them as invalid. Because of this, it might be challenging to precisely identify whether a port is open for nonUDP ports. In the case of UDP ports, a response may be recognized as a clear indicator of an *open* port. A port is judged to be closed if the response is an ICMP port unreachable error.





## 1.2 Early Data **Exploration** and Data Quality Check

Next step is to check the quality of the data. For example, due to the presence of categorical features,  the summary of the data is checked for the types in each category. By doing this, the step needed for data cleaning or to be transformed is identified. For example, checking for missing/empty values.



Following is the list of missing values in percentage:

```
index           0.00
Dur             0.00
RunTime         0.00
Mean            0.00
Sum             0.00
Min             0.00
Max             0.00
Proto           0.00
sTos            0.02
dTos           78.07
sDSb            0.02
dDSb           78.07
sTtl            0.02
dTtl           78.07
sHops           0.02
dHops          78.07
TotPkts         0.00
SrcPkts         0.00
DstPkts         0.00
TotBytes        0.00
SrcBytes        0.00
DstBytes        0.00
Offset          0.00
sMeanPktSz      0.00
dMeanPktSz      0.00
Load            0.00
SrcLoad         0.00
DstLoad         0.00
Loss            0.00
SrcLoss         0.00
DstLoss         0.00
pLoss           0.00
SrcGap         77.13
DstGap         77.13
Rate            0.00
SrcRate         0.00
DstRate         0.00
State           0.00
SrcWin         80.02
DstWin         85.70
sVid           90.68
dVid           99.83
SrcTCPBase     77.13
DstTCPBase     81.43
TcpRtt          0.00
SynAck          0.00
AckDat          0.00
Label           0.00
Attack Type     0.00
dtype: float64
```



Categories per feature and their frequency:

```
_________________________________________

Feature: Proto
  category  freq in %
0      udp      74.39
1      tcp      22.87
2     icmp       2.36
3     sctp       0.38
_________________________________________

Feature: sDSb
  category  freq in %
0      cs0      99.45
1       ef       0.31
2     af11       0.07
3     af41       0.05
4      cs7       0.05
5      cs6       0.03
6     af12       0.01
7       52       0.01
8        4       0.01
9      cs4       0.00
_________________________________________

Feature: State
  category  freq in %
0      REQ      48.94
1      INT      27.06
2      CON      10.55
3      RST       6.13
4      FIN       4.86
5      ECO       2.31
6      ACC       0.10
7      URP       0.04
8      TST       0.01
9      RSP       0.00
_________________________________________

Feature: Label
    category  freq in %
0  Malicious      60.96
1     Benign      39.04
_________________________________________

Feature: Attack Type
         category  freq in %
0          Benign      39.04
1        UDPFlood      37.80
2       HTTPFlood      11.18
3     SlowrateDoS       6.08
4         SYNScan       1.82
5  TCPConnectScan       1.76
6         UDPScan       1.39
7        SYNFlood       0.83
8       ICMPFlood       0.10
_________________________________________
```



The above provides the categorical features and the category per feature with the frequency of occurrence. 

 

![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/pie_benign_malicious_before_cleaning_data.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/15264fa50c8726f62e6867dadcc7f6bcd75ebfbe/Images/pie_benign_malicious_before_cleaning_data.png) 

**Figure 1 - Benign vs Malicious Result - Before Dropping Features with >= 77% Missing Data**



Figure 2 provides the 'Label' ('Y') distribution after removing features with missing values >= 77% followed by removing all entries containing null values and duplicate entries.

![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/pie_benign_malicious_after_cleaning_data.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/4cb8600d4d99876860fa5f876d3ed3c81181f751/Images/pie_benign_malicious_after_cleaning_data.png) 

**Figure 2 - Benign vs Malicious Result - Post Dropping Features with >= 77% & Addressing Missing/Duplicate Entries**



Shape pre & post treating duplicate data:

```
Pre data treatment shape - (49992, 37)
Duplicates : 0
Post data treatment shape - (49992, 37)
```





# 2 Data Preparation

This section provides information on data preparation and cleaning, to allow for analysis as part of this case study and the future case studies covering predictions.  



## 2.1 Data Transformation

Following categorical features were transformed:

**a) [Binary Classification Approach] (Level 1) Target Feature - 'Label' -** Ordinal encoding method used

{'Benign': 0, 'Malicious': 1}.

**b) [Multi-class Classification Approach] (Level 2) Target Feature - 'Attack Type' -** Ordinal encoding method used

{'Benign': 0, 'UDPFlood': 1, 'HTTPFlood': 2, 'SlowrateDoS': 3, 'TCPConnectScan': 4, 'SYNScan': 5, 'UDPScan': 6, 'SYNFlood': 7, 'ICMPFlood': 8}.

**b) Remaining -** 

For the rest of the catagorical data, One-Hot-Encoding method was used.



## 2.2 Data Cleansing

In this step, the data is handled based on the problem found during the data understanding phase. Based on the finding, the following steps are executed:

a) Dropped columns that had >= 77% of missing values. 

b) After step (a), removed rows with NULL values.

c) There was no duplicate data to address upon executing (a) and (b). Note: Original data did have duplicate data.



## 2.2 Final Data (post cleaning and transformation)

The shape data after cleaning : (49992, 37)

In Figure 2, the disbribution of  'Label' distribution between 'benign' or 'melicious' (binary classification) is provided.



![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/benign_malicious_attacktype.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/db7702c944338f1bdd2e8abd73c3d62f8fe3c146/Images/benign_malicious_attacktype.png) 
 
**Figure 3 - Level 2 Target Feature 'Attack Type' ('Y') Post Data Cleaning**

In Figure 3, the disbribution of  'Attack Type' (target feature 'Y' multi-class classification).

Clearly imbalances in the Attack Type categories (classification of malicious attacks). The most noticeable are:

- UDPFlood
- UDPScan
- TCPConnectScan
- SYNScan
- SYNFlood
- ICMPFlood

 

# 3 Data Understanding - Deep Analysis

This section provides information about deeper exploration and analysis of the data conducted, in preparation for future machine learning model.



## 3.1 Exploratory Data Analysis (EDA)

In this section, the results of exploring and visualizing insight from the data is captured.



### 3.1.1 Categorical Data 

Figure 4 provides a view of the categorical features and the category distribution per feature in percentage.

![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/bar_categories.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/bar_categories.png) 
 
**Figure 4 - Categorical Features**

Note:  In Figure 4, the disbribution of the feature categories is presented, providing a hint as to which feature and associated categories may influence 'Label' outcome as 'benign' or 'melicious' (level 1 classification).  



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/proto_benign_malicious.png) 

**Figure 5 - Distribution of Benign and Malicious messages across Proto categories**

Figure 5 provides a view of the message Proto categories and their association to 'Label' classification. For example, 'icmp' protocol based messages have a very high likelihood of being benign. Where as 'tcp' protocol based messages are highly likelihood of being malicious.



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/Proto_benign_malicious_distribution.png) 

**Figure 6 - Comparitive view - Malicious Vs Benign distribution per Proto category**



Figures 5/6 provide a view of the message protocol categories and their association to 'Label' classification. For example, 'icmp' protocol based messages have a very high likelihood of being benign. Where as 'tcp' protocol based messages are highly likely to be of malicious type.



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/State_benign_malicious_distribution.png) 

**Figure 7 - Malicious Vs Benign distribution per State category**

Figure 7 provides a view of the session state categories and their association to 'Label' classification. For example, 'RST', 'FIN' states have a very high likelihood of being malicious. Where as 'ECO' protocol based messages are highly likely to be of benign type.



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/sDSb_benign_malicious_distribution.png) 

**Figure 8 - Malicious Vs Benign distribution per sDSb category**

Figure 8 provides a view of the sDSb categories and their association to 'Label' classification. With the exception of 'cs0', all sDSb types are associated with messsages that are benign. Messages associated with 'cs0' has little less than 2/3 chance of being malicious.



From the distribution presented above, it is clear the following features influence the 'Y' (target feature Label) outcome:

a) From the target feature Label (as 'Y') prespective, the cleaned data is not as imbalanced.

b) From the target feature Attack Type (as 'Y') prespective, the cleaned data is imbalanced. 

b) Over half of the malicious messages are of type 'UDPFlood'.

c) From the 'Proto' feature perspective, message of category type 'tcp' have roughly higher than 95% chance of being malicious. Message of category type 'udp' have roughly higher than 50% chance of being malicious

d) Messages not associated with feature category of type sDSb ''cs0' are benign.



### 3.1.2 Addressing Business Questions

Following were some of the business questions answered based on the analysis of the data.

**1) In the case of malicious messages, what is the most used protocol to launch an attack? - focusing on specific protocol to help prevent majority of the malicious attacks.**

Figure 9 Malicious messages distribution across all Proto feature categories. 



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/attack_type_dist.png) 

**Figure 9 - Malicious message distribution across Proto category types**



Over 70% of the malicious message are based on protocol of type 'udp' . The other protocol use is 'tcp', which is less than 10% of the overall malicious messages.  



**2) Identify the features of an application/appliance to detect/prevent majority of the attacks? **

Lets identify malicious message associated protocol/network features that standout. 



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/proto_attacktypes.png) 

**Figure 10 - Breakdown of malicious message across Attack Type per network protocol**



From Figure 10, it is clear that:

A)  Majority of the attacks are of UDP protocal based UDPFlood attack method

B) In the case of malicious messages using TCP protocol, the attack method utilized are HTTPFlood and SlowrateDoS.



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/sdsb_attacktypes.png) 

**Figure 11 - Breakdown of malicious message across Attack Type per destination diff serve byte value (sDSb)**



From Figure 11, it is clear that:

A)  Majority of the attacks are of sDSb cs0 attacks utilizing SlowrateDoS attack method.

B) Remaining malicious messages utilize SYNScan, TCPConnectiotScan, UDPScan, HTTPFlood, and SlowrateDoS attack methods.



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/state_attacktypes.png) 

**Figure 12 - Breakdown of malicious message across Attack Type per connection state**



From Figure 12 provides the following information:

A)  Majority of the malicious message associated with state REQ & INT use UDPFlood attack methods. 

B) Remaining fewer malicious messages are associated with SYNCScan, TCPConnectScan, UDPScan, SYNCFlood, HTTPFlood, and SlowrateDoS attack method.



In conclusion, application/appliance that can scan UDP protocol to detect anomalies associated with messages using  sDBs and State  can help detect and prevent majority of the malicious attacks.



NOTE: 

1. Please refer to section 2.1 for details description of malicious categories.
2. Please refer to section 2.1 for description of the attack methods.



### 4.1.3 Numerical Features Evaluation 

The numerical features were evaluated via correlation matrix and features with > 80% correlation were dropped. 

```
Features to Drop: ['RunTime', 'Mean', 'Sum', 'Min', 'Max', 'SrcPkts', 'TotBytes', 'SrcBytes', 'DstBytes', 'sMeanPktSz', 'SrcLoad', 'DstLoad', 'Rate', 'SrcRate', 'DstRate']
```

Following are the results after dropping the identified features. 



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/pairplot_numeric_features_label.png) 

**Figure 13 - Pair-plot of features aganist target feature 'Label' ('Y') **

 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/pairplot_numeric_features_attack_type.png) 

**Figure 14 - Pair-plot of features aganist target feature 'Attack Type' ('Y')**

 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/heatmap_numeric_features_encoded.png) 

**Figure 15 - Heatmap of features aganist 'Label' and 'Attack Type'**



### 4.1.3 Observation 

Insights derived from the Initial analysis are: 

a) The most used attack method is UDPFlood followed by HTTPFlood

b) Network protocols per the attach method used are UDP and TCP.

Per the distribution of sDSb Attack Type category, the destination diff serve byte value may help with easily separating messages between benign versus malicious.



### 5.0   Modeling  

The goal of the modeling phase is to identify the best model to be used for identify the key features that dynamically help identify malicious messages. The classification will be executed at two levels:

1. Level 1 - Binary classification where the 'Y' (target feature) is 'Label'

2. Level 2 - Multi-class classification where the 'Y' (target fetaure) is 'Attack Type'.

   

This phase will have four tasks:

**a) Select modeling technique**: Determine which classicication algorithms to try (e.g. KNN,
DT).

**b) Generate test design**: Pending the modeling approach, split the data into training, test, and validation sets.
**c) Build model**: Build and executing the selected models.
**d) Assess model**: Interpret the model results based on the pre-defined success criteria, and the test design.



### 5.1   Model Selection 

The modeling technique is as follows:

### 5.1.1   Pre-process 

The pre-process is defined to transform the categorical features to numerical values,  retaining the original information. As a result, "Ordinal Encoder" was executed against the 'Label' and 'Attack Type' feature since the categorical values had inherent order to it.

For the rest of the features, "OneHotEncoder" was used because the categorical values did not have inherent order or ranking.

Here are the results:

Shape - 49992, 37)

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 49992 entries, 0 to 49991
Data columns (total 37 columns):
 #   Column       Non-Null Count  Dtype  
---  ------       --------------  -----  
 0   level_0      49992 non-null  int64  
 1   Dur          49992 non-null  float64
 2   sTos         49992 non-null  float64
 3   sTtl         49992 non-null  float64
 4   sHops        49992 non-null  float64
 5   TotPkts      49992 non-null  int64  
 6   DstPkts      49992 non-null  int64  
 7   Offset       49992 non-null  int64  
 8   dMeanPktSz   49992 non-null  float64
 9   Load         49992 non-null  float64
 10  Loss         49992 non-null  int64  
 11  DstLoss      49992 non-null  int64  
 12  pLoss        49992 non-null  float64
 13  TcpRtt       49992 non-null  float64
 14  SynAck       49992 non-null  float64
 15  AckDat       49992 non-null  float64
 16  Label        49992 non-null  int64  
 17  Attack Type  49992 non-null  int64  
 18  Proto_icmp   49992 non-null  float64
 19  Proto_sctp   49992 non-null  float64
 20  Proto_tcp    49992 non-null  float64
 21  sDSb_4       49992 non-null  float64
 22  sDSb_52      49992 non-null  float64
 23  sDSb_af11    49992 non-null  float64
 24  sDSb_af12    49992 non-null  float64
 25  sDSb_af41    49992 non-null  float64
 26  sDSb_cs4     49992 non-null  float64
 27  sDSb_cs6     49992 non-null  float64
 28  sDSb_cs7     49992 non-null  float64
 29  State_ACC    49992 non-null  float64
 30  State_CON    49992 non-null  float64
 31  State_FIN    49992 non-null  float64
 32  State_INT    49992 non-null  float64
 33  State_REQ    49992 non-null  float64
 34  State_RSP    49992 non-null  float64
 35  State_RST    49992 non-null  float64
 36  State_TST    49992 non-null  float64
dtypes: float64(29), int64(8)
memory usage: 14.1 MB
None
   level_0       Dur  sTos   sTtl  sHops  TotPkts  DstPkts    Offset  \
0        0  0.000000   0.0   63.0    1.0        1        0   8419356   
1        1  2.578405   0.0   63.0    1.0        2        0   7311480   
2        2  0.000000   0.0   63.0    1.0        1        0  13381224   
3        3  4.455998   0.0  249.0    7.0        2        0  16951584   
4        4  0.000000   0.0   63.0    1.0        1        0  22895580   

   dMeanPktSz        Load  Loss  DstLoss  pLoss  TcpRtt  SynAck  AckDat  \
0         0.0    0.000000     0        0    0.0     0.0     0.0     0.0   
1         0.0  130.313126     0        0    0.0     0.0     0.0     0.0   
2         0.0    0.000000     0        0    0.0     0.0     0.0     0.0   
3         0.0  132.854645     0        0    0.0     0.0     0.0     0.0   
4         0.0    0.000000     0        0    0.0     0.0     0.0     0.0   

   Label  Attack Type  Proto_icmp  Proto_sctp  Proto_tcp  sDSb_4  sDSb_52  \
0      1            1         0.0         0.0        0.0     0.0      0.0   
1      1            1         0.0         0.0        0.0     0.0      0.0   
2      1            1         0.0         0.0        0.0     0.0      0.0   
3      0            0         0.0         0.0        0.0     0.0      0.0   
4      1            1         0.0         0.0        0.0     0.0      0.0   

   sDSb_af11  sDSb_af12  sDSb_af41  sDSb_cs4  sDSb_cs6  sDSb_cs7  State_ACC  \
0        0.0        0.0        0.0       0.0       0.0       0.0        0.0   
1        0.0        0.0        0.0       0.0       0.0       0.0        0.0   
2        0.0        0.0        0.0       0.0       0.0       0.0        0.0   
3        0.0        0.0        0.0       0.0       0.0       0.0        0.0   
4        0.0        0.0        0.0       0.0       0.0       0.0        0.0   

   State_CON  State_FIN  State_INT  State_REQ  State_RSP  State_RST  State_TST  
0        0.0        0.0        0.0        1.0        0.0        0.0        0.0  
1        0.0        0.0        0.0        1.0        0.0        0.0        0.0  
2        0.0        0.0        0.0        1.0        0.0        0.0        0.0  
3        0.0        0.0        1.0        0.0        0.0        0.0        0.0  
4        0.0        0.0        0.0        1.0        0.0        0.0        0.0  
```

### 5.1.2   Modeling Technique 

The models that will be evaluated are:
-  Dummy Classifier as Baseline
-  Logistic Regression
- KNN
- Decision Tree
- SVM  

Following steps were taken to deterime the best model using default hyperparameters:

a) Use of GridSerachCV to help identify the best hyperparameters for each model.

b) Evaluate the accuracy and perfromance of each model. 

The model that performs the best will be selected to identify the important features that contribute to identifying malicious messages and the attack type. 

Becasue the data is imbalanced in the case where 'Y' is the Attack Type, the F1-sore was used.

### 5.1.3   Testing Technique 

The pre-processed data will be split, of which 70% will be randomly allocated for taining and 30% will be allocated for testing.

### 5.1.4   Model assessment using hyperparameter

GridSearchCV will be used for each model to find the optimal hyper parameters.



### 5.1.5   Refining Data -Addressing the Multi-Cornality for Logistic REgression

Per the results presented in Figure 15, following features were further identified to have correlation above 80% were dropped. 

```
Features to Drop: ['Proto_udp', 'sDSb_cs0', 'sDSb_ef', 'State_ECO', 'State_URP']
```



### 5.2   Binary Classification 

### 5.2.1 Summary of Assessment Results 

The dataset was split as follows:

```
Xbin_train shape = (34994, 35)
Xbin_test shape = (14998, 35)
ybin_train shape = (34994,)
ybin_test shape = (14998,)
```

Following is a sample view of the normal data:

...
 | level_0  |  Dur | sTos  |  sTtl  |  sHops  | TotPkts  | DstPkts  | Offset  | dMeanPktSz  | Load  | Loss  | DstLoss  | pLoss  | TcpRtt  | SynAck  | AckDat  | Proto_icmp  | Proto_sctp  | Proto_tcp  | sDSb_4  | sDSb_52  | sDSb_af11  | sDSb_af12  | sDSb_af41  | sDSb_cs4  | sDSb_cs6  | sDSb_cs7  | State_ACC  | State_CON  | State_FIN  | State_INT  | State_REQ  | State_RSP  | State_RST  | State_TST  | 

 | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | 

0 |  -0.758838  | -0.793798 |  -0.06943 |  -0.326517 |  -0.353238 |  -0.008309 |  0.026645 |  -1.121765 |  0.045978 |  -0.006247 |  -0.084809 |  -0.061155 |  -0.093652 |  0.856174 |  0.086611 | 1.347054 | -0.155675 | -0.061767 | 1.831276 | -0.005346 | -0.010692 | -0.025645 | -0.013095 | -0.022046 | -0.005346 | -0.019278 | -0.019278 | -0.032971 | 2.888200 | -0.224424 | -0.606031 | -0.978737 | -0.005346 | -0.257876 | -0.00756
1 | -1.471307 | 1.890357 | -0.06943 | -0.326517 | -0.353238 | -0.111354 | -0.086643 | -0.656525 | -0.283842 | -0.006618 | -0.084809 | -0.061155 | -0.093652 | -0.259800 | -0.043810 | -0.386045 | -0.155675 | -0.061767 | -0.546067 | -0.005346 | -0.010692 | -0.025645 | -0.013095 | -0.022046 | -0.005346 | -0.019278 | -0.019278 | -0.032971 | -0.346236 | -0.224424 | 1.650081 | -0.978737 | -0.005346 | -0.257876 | -0.00756
2 | -1.536618 | -0.807809 | -0.06943 | -0.326517 | -0.353238 | -0.111354 | -0.029999 | 0.063900 | 0.027131 | -0.006618 | -0.084809 | -0.061155 | -0.093652 | 1.029769 | 0.165826 | 1.540303 | -0.155675 | -0.061767 | 1.831276 | -0.005346 | -0.010692 | -0.025645 | -0.013095 | -0.022046 | -0.005346 | -0.019278 | -0.019278 | -0.032971 | -0.346236 | 4.455849 | -0.606031 | -0.978737 | -0.005346 | -0.257876 | -0.00756
3 | 0.966823 | -0.807809 | -0.06943 | -0.326517 | -0.353238 | -0.145702 | -0.086643 | -0.461016 | -0.283842 | -0.006618 | -0.084809 | -0.061155 | -0.093652 | -0.259800 | -0.043810 | -0.386045 | -0.155675 | -0.061767 | -0.546067 | -0.005346 | -0.010692 | -0.025645 | -0.013095 | -0.022046 | -0.005346 | -0.019278 | -0.019278 | -0.032971 | -0.346236 | -0.224424 | 1.650081 | -0.978737 | -0.005346 | -0.257876 | -0.00756
4 | 0.254008 | -0.807809 | -0.06943 | -0.326517 | -0.353238 | -0.145702 | -0.086643 | -0.421553 | -0.283842 | -0.006618 | -0.084809 | -0.061155 | -0.093652 | -0.259800 | -0.043810 | -0.386045 | -0.155675 | -0.061767 | -0.546067 | -0.005346 | -0.010692 | -0.025645 | -0.013095 | -0.022046 | -0.005346 | -0.019278 | -0.019278 | -0.032971 | -0.346236 | -0.224424 | 1.650081 | -0.978737 | -0.005346 | -0.257876 | -0.00756
...



### 5.2.2   Binary Classification - Model Comparison Results

Following is the comparison between the 4 models:

```

                 Model  Train Accuracy  Test Accuracy
0  Dummy Classifier           0.609881       0.609881
1  Logistic Regression        0.961222       0.963462
2                  KNN        1.000000       0.969996
3        Decision Tree        0.984626       0.973063
4                  SVC        0.983883       0.945593
```

```

```

 

 |             |  algorithm  |                     params                          |  mean_score  |  std_score  |                       cv_result                     | 
 |  --------:  |  --------:  |  ------------------------------------------------:  |  ---------:  |  --------:  |  -------------------------------------------------  | 
 |          0  |      LR     |  {'C': 78.47599703514607, 'max_iter': 2500, 'mu...  |   0.960622   |   0.000490  |  {'mean_fit_time': [0.012146790822347006, 0.011...  | 
 |          1  |     KNN     |  {'metric': 'manhattan', 'n_neighbors': 15, 'we...  |   0.971309   |   0.000876  |  {'mean_fit_time': [0.012928485870361328, 0.013...  | 
 |          2  |      DT     |  {'criterion': 'gini', 'max_depth': 10, 'min_sa...  |   0.981940   |   0.001751  |  {'mean_fit_time': [0.03366406758626302, 0.0332...  | 
 |          3  |     SVC     |           {'C': 1000, 'gamma': 1, 'kernel': 'rbf'}  |   0.977568   |   0.001661  |  {'mean_fit_time': [143.36067660649618, 58.6637...  | 


![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/confusion_matrix_binary.png) 

**Figure 16 - Binary Classification - Confusion Matrix**



Figure 16 provides the confusion matrix for the four models with the following additional information per model:

```

Model = LogisticRegression(C=78.47599703514607, max_iter=2500,
                   multi_class='multinomial', solver='sag') AUC = 0.99

Model = KNeighborsClassifier(metric='manhattan', n_neighbors=15, weights='distance') AUC = 1.0

Model = DecisionTreeClassifier(max_depth=10, min_samples_leaf=5) AUC = 0.99

Model = SVC(C=1000, gamma=1, probability=True) AUC = 0.96
```



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/test_best_model_binary_confusion_matrix.png) 

**Figure 17 - Best Model (DecisionTreeClassifier) Confusion Matrix with ROC Plot**



### 5.2.3   Feature engineering and exploration 

 Figure 18 provides the important features selected by the best model.

 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/bin_permutation_importance.png) 

**Figure 18 - Important features selected by the best model**

Base on the results presented in Figure 20, following are the important features identified by the model:

a) Offset  
b) sTtl
c) State_INT
d) sHops
e) TotPkts
f) Proto_icmp
g) Dur
h) Load

These features are identified as important features based on binary classification algorithm and accordingly needs to be analyzed further. Using this results of the analysis, the data can be optimzed to improve the execution of the models.



Lets examine 'Offset', 'sTtl', 'Dur' from the important features selected by the model:



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/offset_density.png) 

**Figure 19 - Benign & Malicious 'Offset' Density**



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/sttl_density.png) 

**Figure 20 - Benign & Malicious 'sTtl' Density**



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/dur_density.png) 

**Figure 21 - Benign & Malicious 'Dur' Density**





### 5.3.   Multi-class Classification

### 5.3.1 Summary of Assessment Results 

The dataset was split as follows:

```
Xmc_train shape = (34994, 35)
Xmc_test shape = (14998, 35)
ymc_train shape = (34994,)
ymc_test shape = (14998,)
```

Following is a sample view of the normal data:

level_0	| 	Dur	| 	sTos	| 	sTtl	| 	sHops	| 	TotPkts	| 	DstPkts	| 	Offset	| 	dMeanPktSz	| 	Load	| 	Loss	| 	DstLoss	| 	pLoss	| 	TcpRtt	| 	SynAck	| 	AckDat	| 	Proto_icmp	| 	Proto_sctp	| 	Proto_tcp	| 	sDSb_4	| 	sDSb_52	| 	sDSb_af11	| 	sDSb_af12	| 	sDSb_af41	| 	sDSb_cs4	| 	sDSb_cs6	| 	sDSb_cs7	| 	State_ACC	| 	State_CON	| 	State_FIN	| 	State_INT	| 	State_REQ	| 	State_RSP	| 	State_RST	| 	State_TST
0	| 	-0.758838	| 	-0.793798	| 	-0.06943	| 	-0.326517	| 	-0.353238	| 	-0.008309	| 	0.026645	| 	-1.121765	| 	0.045978	| 	-0.006247	| 	-0.084809	| 	-0.061155	| 	-0.093652	| 	0.856174	| 	0.086611	| 	1.347054	| 	-0.155675	| 	-0.061767	| 	1.831276	| 	-0.005346	| 	-0.010692	| 	-0.025645	| 	-0.013095	| 	-0.022046	| 	-0.005346	| 	-0.019278	| 	-0.019278	| 	-0.032971	| 	2.888200	| 	-0.224424	| 	-0.606031	| 	-0.978737	| 	-0.005346	| 	-0.257876	| 	-0.00756
1	| 	-1.471307	| 	1.890357	| 	-0.06943	| 	-0.326517	| 	-0.353238	| 	-0.111354	| 	-0.086643	| 	-0.656525	| 	-0.283842	| 	-0.006618	| 	-0.084809	| 	-0.061155	| 	-0.093652	| 	-0.259800	| 	-0.043810	| 	-0.386045	| 	-0.155675	| 	-0.061767	| 	-0.546067	| 	-0.005346	| 	-0.010692	| 	-0.025645	| 	-0.013095	| 	-0.022046	| 	-0.005346	| 	-0.019278	| 	-0.019278	| 	-0.032971	| 	-0.346236	| 	-0.224424	| 	1.650081	| 	-0.978737	| 	-0.005346	| 	-0.257876	| 	-0.00756
2	| 	-1.536618	| 	-0.807809	| 	-0.06943	| 	-0.326517	| 	-0.353238	| 	-0.111354	| 	-0.029999	| 	0.063900	| 	0.027131	| 	-0.006618	| 	-0.084809	| 	-0.061155	| 	-0.093652	| 	1.029769	| 	0.165826	| 	1.540303	| 	-0.155675	| 	-0.061767	| 	1.831276	| 	-0.005346	| 	-0.010692	| 	-0.025645	| 	-0.013095	| 	-0.022046	| 	-0.005346	| 	-0.019278	| 	-0.019278	| 	-0.032971	| 	-0.346236	| 	4.455849	| 	-0.606031	| 	-0.978737	| 	-0.005346	| 	-0.257876	| 	-0.00756
3	| 	0.966823	| 	-0.807809	| 	-0.06943	| 	-0.326517	| 	-0.353238	| 	-0.145702	| 	-0.086643	| 	-0.461016	| 	-0.283842	| 	-0.006618	| 	-0.084809	| 	-0.061155	| 	-0.093652	| 	-0.259800	| 	-0.043810	| 	-0.386045	| 	-0.155675	| 	-0.061767	| 	-0.546067	| 	-0.005346	| 	-0.010692	| 	-0.025645	| 	-0.013095	| 	-0.022046	| 	-0.005346	| 	-0.019278	| 	-0.019278	| 	-0.032971	| 	-0.346236	| 	-0.224424	| 	1.650081	| 	-0.978737	| 	-0.005346	| 	-0.257876	| 	-0.00756
4	| 	0.254008	| 	-0.807809	| 	-0.06943	| 	-0.326517	| 	-0.353238	| 	-0.145702	| 	-0.086643	| 	-0.421553	| 	-0.283842	| 	-0.006618	| 	-0.084809	| 	-0.061155	| 	-0.093652	| 	-0.259800	| 	-0.043810	| 	-0.386045	| 	-0.155675	| 	-0.061767	| 	-0.546067	| 	-0.005346	| 	-0.010692	| 	-0.025645	| 	-0.013095	| 	-0.022046	| 	-0.005346	| 	-0.019278	| 	-0.019278	| 	-0.032971	| 	-0.346236	| 	-0.224424	| 	1.650081	| 	-0.978737	| 	-0.005346	| 	-0.257876	| 	-0.00756



### 5.3.2   Multi-class Classification Model Comparison

Following is the comparison between the 4 models:

```
                 Model  Train Accuracy  Test Accuracy
0  Dummy Classifier           0.390118       0.390118
1  Logistic Regression        0.962622       0.944193
2                  KNN        1.000000       0.965129
3        Decision Tree        0.981654       0.956794
4                  SVC        0.982368       0.940525
```

 |             | algorithm  |                                             params  |  mean_score  |  std_score  |                    cv_result                        | 
 |  --------:  |  -------:  |  ------------------------------------------------:  |  ---------:  |  --------:  |  -------------------------------------------------  | 
 | 0	| 	LR	| 	{'C': 78.47599703514607, 'max_iter': 100, 'mul...	| 	0.962222	| 	0.000385	| 	{'mean_fit_time': [0.012185494105021158, 0.012...
 | 1	| 	KNN	| 	{'metric': 'manhattan', 'n_neighbors': 15, 'we...	| 	0.966880	| 	0.001408	| 	{'mean_fit_time': [0.009124358495076498, 0.012...
 | 2	| 	DT	| 	{'criterion': 'gini', 'max_depth': 10, 'min_sa...	| 	0.979168	| 	0.002174	| 	{'mean_fit_time': [0.03923837343851725, 0.0393...
 | 3	| 	SVC	| 	{'C': 1000, 'gamma': 1, 'kernel': 'rbf'}	| 	0.973881	| 	0.001346	| 	{'mean_fit_time': [202.34143225351968, 42.4139... 







![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/confusion_matrix_multi-class.png) 

**Figure 22 - Multi-class Classification - Confusion Matrix**



Figure 22 provides the confusion matrix for the four models with the following additional information per model:

```

Model = LogisticRegression(C=78.47599703514607, multi_class='multinomial',
                   solver='newton-cg') AUC = 1.0

Model = KNeighborsClassifier(metric='manhattan', n_neighbors=15, weights='distance') AUC = 1.0

Model = DecisionTreeClassifier(max_depth=10, min_samples_leaf=5) AUC = 0.98

Model = SVC(C=1000, gamma=1, probability=True) AUC = 0.99
```





 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/test_best_model_multi-class_confusion_matrix.png) 

**Figure 23 - Best Model (KNN) Confusion Matrix with ROC Plot**



### 5.3.3   Feature engineering and exploration 

 Figure 18 provides the important features selected by the best model.

 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/multi-class_permutation_importance.png) 

**Figure 24 - Important features selected by the best model**

Base on the results presented in Figure 24, following are the important features identified by the model:

a) Offset  
b) sTtl
c) Proto_tcp
d) sHops
d) State_INT
e) Dur

....



Lets examine 'Offset', 'sTls', and 'sHops':

 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/mc_offset_density.png) 

**Figure 25 - Benign & Malicious 'Offset' Density**



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/mc_sttl_density.png) 

**Figure 26 - Benign & Malicious 'sTtl' Density**



 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/mc_shops_density.png) 

**Figure 27 - Benign & Malicious 'sHops' Density**





### 5.3.4   Additional  Evaluation of Binary & Multi-class Classification Models



### 5.3.4.1   Binary Classification Model Evaluation - Target Feature 'Label'

```
LR
              precision    recall  f1-score   support

   Malicious       0.97      0.94      0.95      5851
      Benign       0.96      0.98      0.97      9147

    accuracy                           0.96     14998
   macro avg       0.96      0.96      0.96     14998
weighted avg       0.96      0.96      0.96     14998

KNN
              precision    recall  f1-score   support

   Malicious       0.97      0.95      0.96      5851
      Benign       0.97      0.98      0.98      9147

    accuracy                           0.97     14998
   macro avg       0.97      0.97      0.97     14998
weighted avg       0.97      0.97      0.97     14998

DT
              precision    recall  f1-score   support

   Malicious       0.96      0.97      0.97      5851
      Benign       0.98      0.98      0.98      9147

    accuracy                           0.97     14998
   macro avg       0.97      0.97      0.97     14998
weighted avg       0.97      0.97      0.97     14998

SVC
              precision    recall  f1-score   support

   Malicious       0.91      0.96      0.93      5851
      Benign       0.97      0.94      0.95      9147

    accuracy                           0.95     14998
   macro avg       0.94      0.95      0.94     14998
weighted avg       0.95      0.95      0.95     14998
```





### 5.3.4.2   Multi-class Classification Model Evaluation - Target Feature 'Attack Type'

```
LR
                precision    recall  f1-score   support

      SYNFlood       0.97      0.92      0.95      5851
     HTTPFlood       0.94      1.00      0.97      5705
      UDPFlood       0.98      0.81      0.89      1631
        Benign       0.78      0.98      0.87       907
     ICMPFlood       0.85      0.99      0.91       270
       SYNScan       1.00      0.99      0.99       274
   SlowrateDoS       0.99      1.00      0.99       221
TCPConnectScan       0.97      0.79      0.87       126
       UDPScan       1.00      1.00      1.00        13

      accuracy                           0.94     14998
     macro avg       0.94      0.94      0.94     14998
  weighted avg       0.95      0.94      0.94     14998

KNN
                precision    recall  f1-score   support

      SYNFlood       0.97      0.95      0.96      5851
     HTTPFlood       0.95      0.97      0.96      5705
      UDPFlood       0.97      0.99      0.98      1631
        Benign       0.97      0.96      0.97       907
     ICMPFlood       0.91      0.99      0.95       270
       SYNScan       1.00      0.99      0.99       274
   SlowrateDoS       0.99      1.00      0.99       221
TCPConnectScan       0.97      0.79      0.87       126
       UDPScan       1.00      1.00      1.00        13

      accuracy                           0.97     14998
     macro avg       0.97      0.96      0.96     14998
  weighted avg       0.97      0.97      0.97     14998

DT
                precision    recall  f1-score   support

      SYNFlood       0.97      0.96      0.97      5851
     HTTPFlood       0.96      0.97      0.97      5705
      UDPFlood       0.98      0.86      0.92      1631
        Benign       0.80      0.97      0.88       907
     ICMPFlood       0.90      0.99      0.95       270
       SYNScan       1.00      0.99      0.99       274
   SlowrateDoS       0.99      1.00      0.99       221
TCPConnectScan       1.00      0.79      0.88       126
       UDPScan       0.81      1.00      0.90        13

      accuracy                           0.96     14998
     macro avg       0.93      0.95      0.94     14998
  weighted avg       0.96      0.96      0.96     14998

SVC
                precision    recall  f1-score   support

      SYNFlood       0.91      0.96      0.93      5851
     HTTPFlood       0.96      0.93      0.94      5705
      UDPFlood       0.99      0.90      0.94      1631
        Benign       0.95      0.97      0.96       907
     ICMPFlood       0.91      0.99      0.95       270
       SYNScan       1.00      0.99      0.99       274
   SlowrateDoS       1.00      1.00      1.00       221
TCPConnectScan       1.00      0.79      0.88       126
       UDPScan       1.00      1.00      1.00        13

      accuracy                           0.94     14998
     macro avg       0.97      0.94      0.95     14998
  weighted avg       0.94      0.94      0.94     14998
```



Summarized per class:





'Model: LogisticRegression'

|    | Classes | precision | recall | f1-score | support | 
| --:| ------: | --------: |------: |  -------:| ------  |
| 0 | Benign | 0.974670 | 0.920697 | 0.946915 | 5851  
| 1 | UDPFlood | 0.940642 | 0.997195 | 0.968093 | 5705  
| 2 | HTTPFlood | 0.975646 | 0.810546 | 0.885466 | 1631  
| 3 | SlowrateDoS | 0.780894 | 0.982359 | 0.870117 | 907  
| 4 | TCPConnectScan | 0.848101 | 0.992593 | 0.914676 | 270  
| 5 | SYNScan | 0.996324 | 0.989051 | 0.992674 | 274  
| 6 | UDPScan | 0.986547 | 0.995475 | 0.990991 | 221  
| 7 | SYNFlood | 0.970874 | 0.793651 | 0.873362 | 126  
| 8 | ICMPFlood | 1.000000 | 1.000000 | 1.000000 | 13  



'Model: KNeighborsClassifier'

|    | Classes | precision | recall | f1-score | support | 
| --:| ------: | --------: |------: |  -------:| ------  |
| 0 | Benign | 0.973186 | 0.949069 | 0.960976 | 5851  
| 1 | UDPFlood | 0.954983 | 0.974233 | 0.964512 | 5705  
| 2 | HTTPFlood | 0.968918 | 0.993869 | 0.981235 | 1631 
| 3 | SlowrateDoS | 0.973274 | 0.963616 | 0.968421 | 907  
| 4 | TCPConnectScan | 0.911263 | 0.988889 | 0.948490 | 270 
| 5 | SYNScan | 1.000000 | 0.985401 | 0.992647 | 274  
| 6 | UDPScan | 0.986547 | 0.995475 | 0.990991 | 221  
| 7 | SYNFlood | 0.970588 | 0.785714 | 0.868421 | 126  
| 8 | ICMPFlood | 1.000000 | 1.000000 | 1.000000 | 13  


'Model: DecisionTreeClassifier'

|    | Classes | precision | recall | f1-score | support | 
| --:| ------: | --------: |------: |  -------:| ------  |
| 0 | Benign | 0.969916 | 0.964280 | 0.967089 | 5851  
| 1 | UDPFlood | 0.964105 | 0.969851 | 0.966970 | 5705  
| 2 | HTTPFlood | 0.889509 | 0.977315 | 0.931347 | 1631  
| 3 | SlowrateDoS | 0.950535 | 0.783903 | 0.859215 | 907  
| 4 | TCPConnectScan | 0.902357 | 0.992593 | 0.945326 | 270  
| 5 | SYNScan | 1.000000 | 0.985401 | 0.992647 | 274  
| 6 | UDPScan | 0.986547 | 0.995475 | 0.990991 | 221  
| 7 | SYNFlood | 1.000000 | 0.785714 | 0.880000 | 126  
| 8 | ICMPFlood | 1.000000 | 1.000000 | 1.000000 | 13  


 ![AIML-4G-Apps-Melicious-Attack-Classifiers/Images/proto_benign_malicious.png at main · mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers](https://github.com/mabusamra1/AIML-4G-Apps-Melicious-Attack-Classifiers/blob/main/Images/test_best_model_multi-class_one_vs_one_matrix.png) 

**Figure 28 - Multi-class Classification - One-Vs-One Matrix**







### 6.0   Deployment



### 6.0.1   Summary

- For binary classification, target feature is balanced
- For multi-class classification, target feature is imbalanced. Therefore, examined F1-score.
- All of the models performed well and much better than the baseline. The best model for binary classification is DT while the best model for multi-class classification is KNN.
- DT and KNN performance was very close, therefore for deployment, KNN will be used to predict 'Label' at level 1 and 'Attack Type' at level 2.



### 6.0.2   Recommendation

Further analysis needs to be conducted to improve the performance of the models in terms of execution time. In the case of multi-class classification where the target feature is 'Attack Type', a technique need to be formulated such that when the data is down sampled the result is a balanced data set.



### 7.0   Next Steps

To achieve practical implementation, the code and algorithm must be optimized to process large amounts of data (in Megabytes) in very short period of time (in minutes). Further analysis is required to reduce the number of input features evident from results in section 5.3.3 and 5.2.3.
