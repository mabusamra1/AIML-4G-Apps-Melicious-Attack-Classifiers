# Capstone Project : AIML Appeoach for Securing 4G Applications- Melicious Attack Classification

[Link to notebook:] /prompt_IV_part1.ipynb at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/prompt_IV_part1.ipynb) 



## Context

The goal of this project is to define a self-adaptive secuirty mechanism in 4G/5G cellular networks to detect/prevent attacks launched by cellular devices. The mechanism includes data exploration and quality check of the network generated data and select the best model based on the performance of the classifiers (k-nearest neighbors, logistic regression, decision trees, and support vector machines). The dataset used is related to network intrusion detection generatde over 5G wireless network and comes from [kaggle](https://www.kaggle.com/datasets/humera11/5g-nidd-dataset). 



# 1 Business Understanding



## 1.1 Background



With a plethora of new connections, features, and services introduced, the 5th generation (5G) wireless technology reflects the development of mobile communication networks and is here to stay for the next decade. The multitude of services and technologies that 5G incorporates have made modern com- munication networks very complex and sophisticated in nature. This complexity along with the incorporation of Machine Learn- ing (ML) and Artificial Intelligence (AI) provides the opportunity for the attackers to launch intelligent attacks against the network and network devices. These attacks often traverse undetected due to the lack of intelligent security mechanisms to counter these threats. 

Therefore, the implementation of real-time, proactive, and self-adaptive security mechanisms throughout the network would be an integral part of 5G as well as future communication systems. Large amounts of data collected from real networks will play an important role in the training of AI/ML models to identify and detect malicious content in network traffic. This work presents %G Network Intrusion Detection Dataset (5G-NIDD), a fully labeled dataset built on a functional 5G test network that can be used by those who develop and test AI/ML solutions. The work further analyses the collected data using common ML models and shows the achieved accuracy levels.

The following approach will be taken as part of implementing the self-adaptive security mechanism:

- Level 1 classification - identify cellular device originated messages as 'benign' or 'melicious' taking the binary classification approach 
- Level 2 classification - identify melicious message 'attack type' taking the multi-class classification approach using one-versus-one strategy

The level 1 classification allows the system to detect a threat while level 2 allows the system to take specific steps to neutralize the threat.



## 1.2 Business Goals and KPI

The business objective is to find the best models to identify and detect malicious content in network traffic. This model will help cellular service provides provide secure and reliable services to thier customers, improving business outcomes.



# 2 Data Understanding

This section provides information about the data, its description and is its exploration to make sure it fits the business goals.



## 2.1 **Gathering and Describing Data**

This data comes from [UCI Machine Learning repository Links to an external site.](https://archive.ics.uci.edu/ml/datasets/bank+marketing). 



Here is a sample of the data:



| `Unnamed: 0` |    `Seq` | `Dur` |  `RunTime` |     `Mean` |      `Sum` |      `Min` |      `Max` |    `Proto` | `sTos` |  `dTos` |  `sDSb` | `dDSb` | `sTtl` |  `dTtl` | `sHops` | `dHops` | `Cause` | `TotPkts` | `SrcPkts` | `DstPkts` | `TotBytes` | `SrcBytes` | `DstBytes` | `Offset` | `sMeanPktSz` | `dMeanPktSz` |       `Load` |      `SrcLoad` |     `DstLoad` |         `Loss` | `SrcLoss` | `DstLoss` | `pLoss` | `SrcGap` | `DstGap` | `Rate` |   `SrcRate` |   `DstRate` |    `State` | `SrcWin` | `DstWin` |  `sVid` |  `dVid` | `SrcTCPBase` |   `DstTCPBase` |       `TcpRtt` | `SynAck` | `AckDat` | `Label` | `Attack Type` | `Attack Tool` |          |
| -----------: | -------: | ----: | ---------: | ---------: | ---------: | ---------: | ---------: | ---------: | -----: | ------: | ------: | -----: | -----: | ------: | ------: | ------: | ------: | --------: | --------: | --------: | ---------: | ---------: | ---------: | -------: | -----------: | -----------: | -----------: | -------------: | ------------: | -------------: | --------: | --------: | ------: | -------: | -------: | -----: | ----------: | ----------: | ---------: | -------: | -------: | ------: | ------: | -----------: | -------------: | -------------: | -------: | -------: | ------: | ------------: | ------------: | -------- |
|    `1215885` | `487569` |   `1` | `0.000000` | `0.000000` | `0.000000` | `0.000000` | `0.000000` | `0.000000` | `sctp` | `186.0` | `186.0` |   `ef` |   `ef` | `252.0` | `255.0` |   `4.0` |   `1.0` |  `Status` |       `2` |       `1` |        `1` |      `200` |      `102` |     `98` |     `190300` | `102.000000` |  `98.000000` |     `0.000000` |    `0.000000` |     `0.000000` |       `0` |       `0` |     `0` |    `0.0` |    `NaN` |  `NaN` |  `0.000000` |  `0.000000` | `0.000000` |    `CON` |    `NaN` |   `NaN` | `610.0` |        `NaN` |          `NaN` |          `NaN` |    `0.0` |    `0.0` |   `0.0` |      `Benign` |      `Benign` | `Benign` |
|    `1215886` | `487570` |   `3` | `0.235607` | `0.235607` | `0.235607` | `0.235607` | `0.235607` | `0.235607` | `sctp` | `186.0` |  `40.0` |   `ef` | `af11` | `255.0` | `250.0` |   `1.0` |   `6.0` |  `Status` |       `6` |       `3` |        `3` |     `3056` |      `290` |   `2766` |     `190392` |  `96.666664` | `922.000000` | `69199.984380` | `6587.240723` | `62612.742190` |       `0` |       `0` |     `0` |    `0.0` |    `NaN` |  `NaN` | `21.221781` |  `8.488712` | `8.488712` |    `CON` |    `NaN` |   `NaN` |   `NaN` |      `610.0` |          `NaN` |          `NaN` |    `0.0` |    `0.0` |   `0.0` |      `Benign` |      `Benign` | `Benign` |
|    `1215887` | `487571` | `764` | `0.099927` | `0.099927` | `0.099927` | `0.099927` | `0.099927` | `0.099927` |  `tcp` |   `0.0` |   `0.0` |  `cs0` |  `cs0` |  `64.0` | `114.0` |   `0.0` |  `14.0` |   `Start` |       `3` |       `2` |        `1` |      `252` |      `160` |     `92` |     `190496` |  `80.000000` |  `92.000000` |  `6404.675293` | `6404.675293` |     `0.000000` |       `0` |       `0` |     `0` |    `0.0` |    `0.0` |  `0.0` | `20.014610` | `10.007305` | `0.000000` |    `CON` |  `213.0` | `273.0` |   `NaN` |        `NaN` | `2.237373e+09` | `1.983280e+09` |    `0.0` |    `0.0` |   `0.0` |      `Benign` |      `Benign` | `Benign` |
|    `1215888` | `487572` |   `3` | `1.307852` | `1.307852` | `1.307852` | `1.307852` | `1.307852` | `1.307852` | `sctp` | `186.0` |  `40.0` |   `ef` | `af11` | `255.0` | `250.0` |   `1.0` |   `6.0` |  `Status` |       `6` |       `3` |        `3` |      `596` |      `306` |    `290` |     `190704` | `102.000000` |  `96.666664` |  `2434.526123` | `1247.847534` |  `1186.678589` |       `0` |       `0` |     `0` |    `0.0` |    `NaN` |  `NaN` |  `3.823062` |  `1.529225` | `1.529225` |    `CON` |    `NaN` |   `NaN` |   `NaN` |      `610.0` |          `NaN` |          `NaN` |    `0.0` |    `0.0` |   `0.0` |      `Benign` |      `Benign` | `Benign` |
|    `1215889` | `487573` |   `1` | `0.476803` | `0.476803` | `0.476803` | `0.476803` | `0.476803` | `0.476803` | `sctp` | `186.0` | `186.0` |   `ef` |   `ef` | `252.0` | `255.0` |   `4.0` |   `1.0` |  `Status` |       `4` |       `2` |        `2` |      `392` |      `200` |    `192` |     `190808` | `100.000000` |  `96.000000` |  `3288.569824` | `1677.841797` |  `1610.728149` |       `0` |       `0` |     `0` |    `0.0` |    `NaN` |  `NaN` |  `6.291907` |  `2.097302` | `2.097302` |    `CON` |    `NaN` |   `NaN` | `610.0` |        `NaN` |          `NaN` |          `NaN` |    `0.0` |    `0.0` |   `0.0` |      `Benign` |      `Benign` | `Benign` |



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





A sample set of size 100K was randomly selected to represent the 1.2M entries, because of the cost of processing 1.2M entries in terms of high CPU processing power and more importantly the time it takes (3+ weeks) to evaluate and select the suitable model.



Upon closely examining the data, following features were removed since they were not relevent to 'Y' (i.e., they were intriduced by Argus tool as part of message flow generation) :

- Unnamed, Seq, Cause, and Attack Tool.

  Note: the index was reset.



Here is want the samlple data of the randomly selected 100K entires post removal of features not related to 'Y':

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 100000 entries, 0 to 99999
Data columns (total 49 columns):
 #   Column       Non-Null Count   Dtype  
---  ------       --------------   -----  
 0   index        100000 non-null  int64  
 1   Dur          100000 non-null  float64
 2   RunTime      100000 non-null  float64
 3   Mean         100000 non-null  float64
 4   Sum          100000 non-null  float64
 5   Min          100000 non-null  float64
 6   Max          100000 non-null  float64
 7   Proto        100000 non-null  object 
 8   sTos         99976 non-null   float64
 9   dTos         22347 non-null   float64
 10  sDSb         99976 non-null   object 
 11  dDSb         22347 non-null   object 
 12  sTtl         99976 non-null   float64
 13  dTtl         22347 non-null   float64
 14  sHops        99976 non-null   float64
 15  dHops        22347 non-null   float64
 16  TotPkts      100000 non-null  int64  
 17  SrcPkts      100000 non-null  int64  
 18  DstPkts      100000 non-null  int64  
 19  TotBytes     100000 non-null  int64  
 20  SrcBytes     100000 non-null  int64  
 21  DstBytes     100000 non-null  int64  
 22  Offset       100000 non-null  int64  
 23  sMeanPktSz   100000 non-null  float64
 24  dMeanPktSz   100000 non-null  float64
 25  Load         100000 non-null  float64
 26  SrcLoad      100000 non-null  float64
 27  DstLoad      100000 non-null  float64
 28  Loss         100000 non-null  int64  
 29  SrcLoss      100000 non-null  int64  
 30  DstLoss      100000 non-null  int64  
 31  pLoss        100000 non-null  float64
 32  SrcGap       22824 non-null   float64
 33  DstGap       22824 non-null   float64
 34  Rate         100000 non-null  float64
 35  SrcRate      100000 non-null  float64
 36  DstRate      100000 non-null  float64
 37  State        100000 non-null  object 
 38  SrcWin       19818 non-null   float64
 39  DstWin       14418 non-null   float64
 40  sVid         9608 non-null    float64
 41  dVid         159 non-null     float64
 42  SrcTCPBase   22824 non-null   float64
 43  DstTCPBase   18837 non-null   float64
 44  TcpRtt       100000 non-null  float64
 45  SynAck       100000 non-null  float64
 46  AckDat       100000 non-null  float64
 47  Label        100000 non-null  object 
 48  Attack Type  100000 non-null  object 
dtypes: float64(32), int64(11), object(6)
memory usage: 37.4+ MB
```

```
              index            Dur        RunTime           Mean  \
count  1.000000e+05  100000.000000  100000.000000  100000.000000   
mean   6.079342e+05       1.363501       1.363501       1.363501   
std    3.519268e+05       1.688935       1.688935       1.688935   
min    0.000000e+00       0.000000       0.000000       0.000000   
25%    3.024070e+05       0.000000       0.000000       0.000000   
50%    6.075380e+05       0.000000       0.000000       0.000000   
75%    9.135062e+05       2.580313       2.580313       2.580313   
max    1.215888e+06      19.630236      19.630236      19.630236   

                 Sum            Min            Max          sTos  \
count  100000.000000  100000.000000  100000.000000  99976.000000   
mean        1.363501       1.363501       1.363501      0.827689   
std         1.688935       1.688935       1.688935     12.211587   
min         0.000000       0.000000       0.000000      0.000000   
25%         0.000000       0.000000       0.000000      0.000000   
50%         0.000000       0.000000       0.000000      0.000000   
75%         2.580313       2.580313       2.580313      0.000000   
max        19.630236      19.630236      19.630236    224.000000   

               dTos          sTtl          dTtl         sHops         dHops  \
count  22347.000000  99976.000000  22347.000000  99976.000000  22347.000000   
mean       2.582539     81.802082     65.292209      2.275696      5.022732   
std       20.859433     56.403271     27.892751      3.593459      2.281658   
min        0.000000     36.000000     41.000000      0.000000      0.000000   
25%        0.000000     63.000000     59.000000      1.000000      5.000000   
50%        0.000000     63.000000     59.000000      1.000000      5.000000   
75%        0.000000     63.000000     59.000000      1.000000      5.000000   
max      186.000000    255.000000    255.000000     28.000000     45.000000   

             TotPkts       SrcPkts       DstPkts      TotBytes       SrcBytes  \
count  100000.000000  100000.00000  100000.00000  1.000000e+05  100000.000000   
mean        5.106650       3.68305       1.42360  3.598969e+03    2506.141530   
std        24.604368      18.29323      11.96787  2.971134e+04   24209.952112   
min         1.000000       0.00000       0.00000  4.200000e+01       0.000000   
25%         1.000000       1.00000       0.00000  4.200000e+01      42.000000   
50%         2.000000       1.00000       0.00000  8.400000e+01      74.000000   
75%         2.000000       2.00000       0.00000  8.400000e+01      84.000000   
max      2732.000000     673.00000    2059.00000  3.028111e+06  683182.000000   

           DstBytes        Offset     sMeanPktSz     dMeanPktSz          Load  \
count  1.000000e+05  1.000000e+05  100000.000000  100000.000000  1.000000e+05   
mean   1.092828e+03  1.236100e+07      73.873508      61.215904  7.362111e+06   
std    1.629788e+04  1.068968e+07     145.323400     213.562290  7.250058e+08   
min    0.000000e+00  1.280000e+02       0.000000       0.000000  0.000000e+00   
25%    0.000000e+00  3.061331e+06      42.000000       0.000000  0.000000e+00   
50%    0.000000e+00  9.860672e+06      42.000000       0.000000  0.000000e+00   
75%    0.000000e+00  1.908555e+07      67.000000       0.000000  1.305194e+02   
max    2.935754e+06  3.968801e+07    1392.000000    1465.833374  8.619200e+10   

            SrcLoad       DstLoad           Loss        SrcLoss  \
count  1.000000e+05  1.000000e+05  100000.000000  100000.000000   
mean   1.804870e+05  7.181624e+06       0.022680       0.013500   
std    1.397924e+07  7.120108e+08       0.229665       0.171925   
min    0.000000e+00  0.000000e+00       0.000000       0.000000   
25%    0.000000e+00  0.000000e+00       0.000000       0.000000   
50%    0.000000e+00  0.000000e+00       0.000000       0.000000   
75%    1.304916e+02  0.000000e+00       0.000000       0.000000   
max    2.112000e+09  8.408000e+10      13.000000       6.000000   

             DstLoss          pLoss        SrcGap        DstGap          Rate  \
count  100000.000000  100000.000000  22824.000000  22824.000000  1.000000e+05   
mean        0.009180       0.363532      0.142131      2.463722  1.332903e+03   
std         0.149184       3.758572     20.298604    232.631385  1.052228e+05   
min         0.000000       0.000000      0.000000      0.000000  0.000000e+00   
25%         0.000000       0.000000      0.000000      0.000000  0.000000e+00   
50%         0.000000       0.000000      0.000000      0.000000  0.000000e+00   
75%         0.000000       0.000000      0.000000      0.000000  3.886160e-01   
max         7.000000      60.000000   3064.000000  32976.000000  1.300000e+07   

            SrcRate       DstRate        SrcWin        DstWin    sVid   dVid  \
count  1.000000e+05  1.000000e+05  1.981800e+04  1.441800e+04  9608.0  159.0   
mean   3.325112e+02  7.494301e+02  9.667513e+05  6.975303e+04   610.0  610.0   
std    2.683709e+04  6.847293e+04  5.149044e+06  1.960537e+05     0.0    0.0   
min    0.000000e+00  0.000000e+00  0.000000e+00  0.000000e+00   610.0  610.0   
25%    0.000000e+00  0.000000e+00  5.657600e+04  6.476800e+04   610.0  610.0   
50%    0.000000e+00  0.000000e+00  6.259200e+04  6.489600e+04   610.0  610.0   
75%    3.883370e-01  0.000000e+00  6.425600e+04  6.502400e+04   610.0  610.0   
max    4.000000e+06  8.000000e+06  3.355392e+07  8.340480e+06   610.0  610.0   

         SrcTCPBase    DstTCPBase         TcpRtt         SynAck         AckDat  
count  2.282400e+04  1.883700e+04  100000.000000  100000.000000  100000.000000  
mean   2.042588e+09  2.137738e+09       0.004668       0.000555       0.004113  
std    1.233011e+09  1.241607e+09       0.016869       0.012186       0.010753  
min    1.509510e+05  2.599570e+05       0.000000       0.000000       0.000000  
25%    9.776496e+08  1.054640e+09       0.000000       0.000000       0.000000  
50%    1.994167e+09  2.158072e+09       0.000000       0.000000       0.000000  
75%    3.079786e+09  3.207978e+09       0.000000       0.000000       0.000000  
max    4.294967e+09  4.294824e+09       1.051156       1.024680       0.266729  
```





***Here are some additional details on target columns - <u>'Label' and 'Attack Type'</u>:***

**1 - *DoS Attacks* Types -** A DoS attack is one of the most common attacks that can occur in a network. The aim of this attack is to slow down or completely shut down a target making it inaccessible to legitimate users. Flooding techniques and malicious content injection are some of the common methods to lunch a DoS attack. The network or a node will eventually undergo resource exhaustion and deny the nonmalicious users’ access as a result of a DoS attack. Due to the heterogeneous nature of the 5G networks, DoS attacks impose a vital threat in 5G which may target the network nodes, devices, and applications.

​	**a) *Benign Traffic:*** The benign traffic profile includes protocols such as HTTP, HTTPS, SSH, and Secure File Transfer Protocol (SFTP). 

​	**b) *ICMP Flood:*** Internet Control Message Protocol (ICMP) flood attacks use ICMP echo requests to flood a target at a very high frequency. Ideally, an ICMP echo reply follows the echo request to the same Internet Protocol (IP) address. In this type of attack, the target will send back echo replies to massive amounts of ICMP echo requests. The higher frequency of echo requests also leads to a higher frequency in the rate of response which eventually overwhelms the network and makes the services unavailable for normal users.

​	**c) *UDP Flood:*** In a User Datagram Protocol (UDP) flood attack, attacker sends UDP packets at a higher rate. Since UDP is a connection-less protocol, it is possible to send a large amount of traffic. As the UDP packets arrive at the target destination, the reply is a “Destination Unreachable” packet if no associated application is found. Over time, as a higher amount of UDP packets are received and responded to, the system eventually becomes nonresponsive.

​	**d) *SYN Flood:*** SYN flood attack is a result of the exploitation of the TCP three way handshake. In a typical TCP communication between two nodes, the source nodes sends a SYN packet to the desired node for the initiation of the connection. The destination node replies with a SYN ACK to acknowledge the SYN packet. Finally, the source sends another ACK to acknowledge receiving the SYN ACK, completing the three way handshake. In a SYN flood attack, the attacker does not perform the final step of the TCP handshake, therefore leaving the connection half open. The transmission of SYN packets at a higher frequency will leave large amounts of ports half open for a certain period and eventually the receiver will be exhausted once all ports are occupied preventing access for legitimate users.

​	**e) *HTTP Flood:*** HTTP flood attacks target the application layer. It is a popular method for DoS/DDoS attacks due to its proven effectiveness in mimicking normal human behavior and thereby staying undetected. We used Python based Goldeneye tool to conduct the HTTP flood attacks. To perform the application layer attacks, we deployed a web server at the victim Multi-access Edge Computing (MEC) instance. The target was an Apache2 web server deployed in MEC.

​	**f) *Slowrate DoS:*** Another exploitation of the application layer to conduct DoS attacks is the use of slow rate attacks. In terms of the speed and the number of packets directed at the target, it is comparatively different from other forms of DoS attacks. This slow nature of the traffic makes it harder to detect. In this exercise, we conducted two different forms of slow rate DoS attacks. As the first one, we performed slowloris attack through a python script. The attack establishes several connections with the targeted web server and maintain them for a longer period. We performed this by sending HTTP partial headers continuously to keep the connections open without completion. The web server waits for the connections to complete which might never occur. The opening of a large number of such connections will eventually lead to resource exhaustion. 

​	In another case, the attacker sends slow POST requests to a web server. The POST requests comprises packets that specify a larger packet size in the header field, but the actual packet has a lesser size. The server then waits for the completion of the whole packet size specified in the header field.



**2 - *Port Scans*** - A port scan usually precedes an actual attack to identify opportunities for attacks via open ports. Typically, port scans send requests to a targeted range of ports in a targeted host and observe the response. The response is sufficient to determine the status of a specific port in most cases. In some instances, deeper knowledge such as the operating system of the target may also be discovered. Port scan is an efficient way to determine exploitable hosts in a network before the execution of attacks. The dataset contains attack data from different port scans such as the SYN scan, TCP Connect scan, and UDP scan.

​	**a) *SYN Scan:*** The SYN scan uses part of the three way handshake in TCP connection establishment to discover open ports. The attacker sets the SYN flag in a TCP packet and sends to the target. If the targeted port/s is ready for a TCP connection, it returns a response packet with SYN and ACK flags set. This means the scan indicates an *open* port to the attacker. Ports that are not ready to establish a TCP connection send a RST packet indicating a *closed* port. As the attacker determines the state of the port from two packet flows, attacker cease the execution of the next step of the three way handshake. However, to terminate the connection the attacker may send an RST packet to the target once the information on the status of the port is collected. If not, the target will keep sending packets with SYN and ACK flags set until a response is seen from the attacker. Other than *open* or *closed* ports, a *filtered* port may imply that a firewall is blocking the packets or the host is not reachable.

​	The incomplete three way handshake in SYN scan makes the scanning process quite fast in comparison to other available techniques. The SYN scan is one of the most popular scanning techniques.

​	**b) *TCP Connect Scan:*** Similar to SYN scan, the TCP connect scan exploits the TCP handshake to perform the scanning process. However, the three way handshake is fully completed therefore, the time taken to scan the ports is higher compared with SYN Scan. Conversely, attackers may not need the same level of privileges to execute a TCP connect scan as they require for SYN scan.

​	The execution of the TCP connect scan is similar to SYN scan with the addition of the completion step in the three way handshake. This means that the two initial packet flows (SYN flag set packet and SYN ACK flags set packet) take place for an *open* port. Subsequently, the target replies with a packet set with ACK flag to complete the three way handshake. Although the opening of a TCP connection also offers the potential for data exchange, the attacking operating system makes sure the connection is terminated as soon as it detects that one has been made. In the event of a *closed* port, target sends a RST packet to the host similar to the SYN scan. *Filtered* ports may also exist in this scenario.

​	**c) *UDP Scan:*** UDP scan transmits UDP datagrams to the targeted ports of the targeted host. The attacker sends the UDP packets with a missing payload to ports that are not UDP. For UDP ports, a protocol-specific payload will exist. In UDP scan, the status of a port is defined based on the response of the target or the unresponsiveness of the target. As nonUDP ports receive a UDP datagram without a payload, the probability of getting a proper response is minimum. An *open|filtered* state is likely from such ports which indicates either a firewall is blocking the packets or packets are simply been forwarded from TCP/IP stack towards a listening application and discards them as invalid. Because of this, it might be challenging to precisely identify whether a port is open for nonUDP ports. In the case of UDP ports, a response may be recognized as a clear indicator of an *open* port. A port is judged to be closed if the response is an ICMP port unreachable error.





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
dTos           77.65
sDSb            0.02
dDSb           77.65
sTtl            0.02
dTtl           77.65
sHops           0.02
dHops          77.65
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
SrcGap         77.18
DstGap         77.18
Rate            0.00
SrcRate         0.00
DstRate         0.00
State           0.00
SrcWin         80.18
DstWin         85.58
sVid           90.39
dVid           99.84
SrcTCPBase     77.18
DstTCPBase     81.16
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
0        udp      74.36
1        tcp      22.83
2       icmp       2.45
3       sctp       0.36
4  ipv6-icmp       0.00
_________________________________________

Feature: sDSb
   category  freq in %
0       cs0      99.49
1        ef       0.29
2      af11       0.06
3       cs6       0.05
4      af41       0.04
5       cs7       0.03
6      af12       0.01
7        52       0.01
8       cs4       0.01
9         4       0.00
10       39       0.00
_________________________________________

Feature: State
   category  freq in %
0       REQ      48.31
1       INT      27.26
2       CON      10.81
3       RST       6.32
4       FIN       4.75
5       ECO       2.39
6       ACC       0.09
7       URP       0.06
8       RSP       0.00
9       TST       0.00
10      NRS       0.00
_________________________________________

Feature: Label
    category  freq in %
0  Malicious      60.58
1     Benign      39.42
_________________________________________

Feature: Attack Type
         category  freq in %
0          Benign      39.42
1        UDPFlood      37.55
2       HTTPFlood      11.61
3     SlowrateDoS       5.96
4         SYNScan       1.65
5  TCPConnectScan       1.63
6         UDPScan       1.32
7        SYNFlood       0.76
8       ICMPFlood       0.11
_________________________________________
```



The above provides the categorical features and the category per feature with the frequency of occurrence. 

 

![AIML-Portfolio-Melicious-Attack-Classifiers/images/pie_benign_malicious_before_cleaning_data.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/pie_benign_malicious_before_cleaning_data.png) 

**Figure 1 - Benign vs Malicious Result - Before Dropping Features with >= 77% Missing Data**



Figure 2 provides the 'Label' ('Y') distribution after removing features with missing values >= 77% followed by removing all entries containing null values and duplicate entries.

![AIML-Portfolio-Melicious-Attack-Classifiers/images/pie_benign_malicious_after_cleaning_data.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/pie_benign_malicious_after_cleaning_data.png) 

**Figure 2 - Benign vs Malicious Result - Post Dropping Features with >= 77% & Addressing Missing/Duplicate Entries**



Shape pre & post treating duplicate data:

```
Pre data treatment shape - (99976, 37)
Duplicates : 0
Post data treatment shape - (99976, 37)
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

The shape data after cleaning : (99976, 37)

In Figure 2, the disbribution of  'Label' distribution between 'benign' or 'melicious' (binary classification) is provided.



![AIML-Portfolio-Melicious-Attack-Classifiers/images/benign_malicious_attacktype.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/benign_malicious_attacktype.png) 

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

![AIML-Portfolio-Melicious-Attack-Classifiers/images/bar_categories.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/bar_categories.png) 

**Figure 4 - Categorical Features**

Note:  In Figure 3, the disbribution of the feature categories is presented, providing a hint as to which feature and associated categories may influence 'Label' outcome as 'benign' or 'melicious' (level 1 classification).  



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/proto_benign_malicious.png) 

**Figure 5 - Distribution of Benign and Malicious messages across Proto categories**

Figure 5 provides a view of the message Proto categories and their association to 'Label' classification. For example, 'icmp' protocol based messages have a very high likelihood of being benign. Where as 'tcp' protocol based messages are highly likelihood of being malicious.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/Proto_benign_malicious_distribution.png) 

**Figure 6 - Comparitive view - Malicious Vs Benign distribution per Proto category**



Figure 5/6 provides a view of the message protocol categories and their association to 'Label' classification. For example, 'icmp' protocol based messages have a very high likelihood of being benign. Where as 'tcp' protocol based messages are highly likely to be of malicious type.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/State_benign_malicious_distribution.png) 

**Figure 7 - Malicious Vs Benign distribution per State category**

Figure 7 provides a view of the session state categories and their association to 'Label' classification. For example, 'RST', 'FIN' states have a very high likelihood of being malicious. Where as 'ECO' protocol based messages are highly likely to be of benign type.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/sDSb_benign_malicious_distribution.png) 

**Figure 8 - Malicious Vs Benign distribution per sDSb category**

Figure 8 provides a view of the sDSb categories and their association to 'Label' classification. With the exception of 'cs0', all sDSb types are associated with messsages that are benign. Messages associated with 'cs0' has little less than 2/3 chance of being malicious.



From the distribution presented above, it is clear the following features influence the 'Y' (target feature Label) outcome:

a) From the target feature Label (as 'Y') prespective, the cleaned data is not as imbalanced.

b) From the target feature Attack Type (as 'Y') prespective, the cleaned data is imbalanced. 

b) Over half of the malicious messages are of type 'UDPFlood'.

c) From the 'Proto' feature perspective, message of category type 'tcp' have roughly higher than 95% chance of being malicious. Message of category type 'dup' have roughly higher than 50% chance of being malicious

d) Messages not associated with feature category of type sDSb ''cs0' are benign.



### 3.1.2 Addressing Business Questions

Following were some of the business questions answered based on the analysis of the data.

**1) In the case of malicious messages, what is the most used protocol to launch an attack? - focusing on specific protocol to help prevent majority of the malicious attacks.**

Figure 9 Malicious messages distribution across all Proto feature categories. 



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/attack_type_dist.png) 

**Figure 9 - Malicious message distribution across Proto category types**



Over 70% of the malicious message are based on protocol of type 'udp' . The other protocol use is 'tcp', which is less than 10% of the overall malicious messages.  



**2) Identify the features of an application/appliance to detect/prevent majority of the attacks? **

Lets identify malicious message associated protocol/network features that standout. 



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/proto_attacktypes.png) 

**Figure 10 - Breakdown of malicious message across Attack Type per network protocol**



From Figure 10, it is clear that:

A)  Majority of the attacks are of UDP protocal based UDPFlood attack method

B) In the case of malicious messages using TCP protocol, the attack method utilized are HTTPFlood and SlowrateDoS.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/sdsb_attacktypes.png) 

**Figure 11 - Breakdown of malicious message across Attack Type per destination diff serve byte value (sDSb)**



From Figure 11, it is clear that:

A)  Majority of the attacks are of sDSb cs0 attacks utilizing SlowrateDoS attack method.

B) Remaining malicious messages utilize SYNScan, TCPConnectiotScan, UDPScan, HTTPFlood, and SlowrateDoS attack methods.



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/state_attacktypes.png) 

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



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/pairplot_numeric_features_label.png) 

**Figure 13 - Pair-plot of features aganist target feature 'Label' ('Y') **

 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/pairplot_numeric_features_attack_type.png) 

**Figure 14 - Pair-plot of features aganist target feature 'Attack Type' ('Y')**

 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/heatmap_numeric_features_encoded.png) 

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

Shape - 99976, 39)

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 99976 entries, 0 to 99975
Data columns (total 39 columns):
 #   Column           Non-Null Count  Dtype  
---  ------           --------------  -----  
 0   level_0          99976 non-null  int64  
 1   Dur              99976 non-null  float64
 2   sTos             99976 non-null  float64
 3   sTtl             99976 non-null  float64
 4   sHops            99976 non-null  float64
 5   TotPkts          99976 non-null  int64  
 6   DstPkts          99976 non-null  int64  
 7   Offset           99976 non-null  int64  
 8   dMeanPktSz       99976 non-null  float64
 9   Load             99976 non-null  float64
 10  Loss             99976 non-null  int64  
 11  SrcLoss          99976 non-null  int64  
 12  DstLoss          99976 non-null  int64  
 13  pLoss            99976 non-null  float64
 14  TcpRtt           99976 non-null  float64
 15  SynAck           99976 non-null  float64
 16  AckDat           99976 non-null  float64
 17  Label            99976 non-null  int64  
 18  Attack Type      99976 non-null  int64  
 19  Proto_icmp       99976 non-null  float64
 20  Proto_ipv6-icmp  99976 non-null  float64
 21  Proto_sctp       99976 non-null  float64
 22  Proto_tcp        99976 non-null  float64
 23  sDSb_4           99976 non-null  float64
 24  sDSb_52          99976 non-null  float64
 25  sDSb_af11        99976 non-null  float64
 26  sDSb_af12        99976 non-null  float64
 27  sDSb_af41        99976 non-null  float64
 28  sDSb_cs4         99976 non-null  float64
 29  sDSb_cs6         99976 non-null  float64
 30  sDSb_cs7         99976 non-null  float64
 31  State_ACC        99976 non-null  float64
 32  State_CON        99976 non-null  float64
 33  State_FIN        99976 non-null  float64
 34  State_INT        99976 non-null  float64
 35  State_REQ        99976 non-null  float64
 36  State_RSP        99976 non-null  float64
 37  State_RST        99976 non-null  float64
 38  State_TST        99976 non-null  float64
dtypes: float64(30), int64(9)
memory usage: 29.7 MB
None
   level_0       Dur  sTos  sTtl  sHops  TotPkts  DstPkts    Offset  \
0        0  4.564231   0.0  63.0    1.0        3        0  12409860   
1        1  0.000000   0.0  63.0    1.0        1        0  12002540   
2        2  2.584038   0.0  63.0    1.0        2        0  20161452   
3        3  2.586121   0.0  63.0    1.0        2        0   3481588   
4        4  4.987077   0.0  64.0    0.0       43       21   2044388   

    dMeanPktSz          Load  Loss  SrcLoss  DstLoss  pLoss    TcpRtt  \
0     0.000000    147.231812     0        0        0    0.0  0.000000   
1     0.000000      0.000000     0        0        0    0.0  0.000000   
2     0.000000    130.029053     0        0        0    0.0  0.000000   
3     0.000000    129.924316     0        0        0    0.0  0.000000   
4  1217.238037  44908.066410     0        0        0    0.0  0.034837   

     SynAck    AckDat  Label  Attack Type  Proto_icmp  Proto_ipv6-icmp  \
0  0.000000  0.000000      1            1         0.0              0.0   
1  0.000000  0.000000      1            1         0.0              0.0   
2  0.000000  0.000000      0            0         0.0              0.0   
3  0.000000  0.000000      1            1         0.0              0.0   
4  0.020551  0.014286      0            0         0.0              0.0   

   Proto_sctp  Proto_tcp  sDSb_4  sDSb_52  sDSb_af11  sDSb_af12  sDSb_af41  \
0         0.0        0.0     0.0      0.0        0.0        0.0        0.0   
1         0.0        0.0     0.0      0.0        0.0        0.0        0.0   
2         0.0        0.0     0.0      0.0        0.0        0.0        0.0   
3         0.0        0.0     0.0      0.0        0.0        0.0        0.0   
4         0.0        1.0     0.0      0.0        0.0        0.0        0.0   

   sDSb_cs4  sDSb_cs6  sDSb_cs7  State_ACC  State_CON  State_FIN  State_INT  \
0       0.0       0.0       0.0        0.0        0.0        0.0        0.0   
1       0.0       0.0       0.0        0.0        0.0        0.0        0.0   
2       0.0       0.0       0.0        0.0        0.0        0.0        0.0   
3       0.0       0.0       0.0        0.0        0.0        0.0        1.0   
4       0.0       0.0       0.0        0.0        1.0        0.0        0.0   

   State_REQ  State_RSP  State_RST  State_TST  
0        1.0        0.0        0.0        0.0  
1        1.0        0.0        0.0        0.0  
2        1.0        0.0        0.0        0.0  
3        0.0        0.0        0.0        0.0  
4        0.0        0.0        0.0        0.0  
```

### 5.1.2   Modeling Technique 

The models that will be evaluated are:

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



### 5.1.5   Refining Data

Per the results presented in Figure 15, following features were further identified to have correlation above 80% were dropped:

```
Features to Drop: ['Proto_udp', 'sDSb_39', 'sDSb_cs0', 'sDSb_ef', 'State_ECO', 'State_NRS', 'State_URP']
```



### 5.2   Binary Classification 

### 5.2.1 Summary of Assessment Results 

The dataset was split as follows:

```
Xbin_train shape = (69983, 37)
 Xbin_test shape = (29993, 37)
ybin_train shape = (69983,)
 ybin_test shape = (29993,)
```

Following is a sample view of the normal data:

|      |   level_0 |       Dur |      sTos |      sTtl |     sHops |   TotPkts |   DstPkts |    Offset | dMeanPktSz |      Load |      Loss |   SrcLoss |   DstLoss |     pLoss |    TcpRtt |    SynAck |    AckDat | Proto_icmp | Proto_ipv6-icmp | Proto_sctp | Proto_tcp |   sDSb_4 |   sDSb_52 | sDSb_af11 | sDSb_af12 | sDSb_af41 |  sDSb_cs4 |  sDSb_cs6 |  sDSb_cs7 | State_ACC | State_CON | State_FIN | State_INT | State_REQ | State_RSP | State_RST | State_TST |
| ---: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | ---------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | ---------: | --------------: | ---------: | --------: | -------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: |
|    0 | -0.294618 |  0.720003 | -0.069182 | -0.333087 | -0.353128 | -0.122447 | -0.111416 |  0.693212 |  -0.286001 | -0.010133 | -0.100388 | -0.080038 | -0.062391 | -0.098954 | -0.274138 | -0.045576 | -0.381555 |  -0.157929 |        -0.00378 |  -0.061184 | -0.542983 | -0.00756 | -0.010692 | -0.027005 | -0.010692 | -0.020006 | -0.006547 | -0.022369 | -0.020006 | -0.031642 | -0.346897 | -0.223800 | -0.609654 |  1.029838 |  -0.00756 | -0.259771 |  -0.00378 |
|    1 |  0.829196 |  1.903937 | -0.069182 | -0.333087 | -0.353128 | -0.122447 | -0.111416 | -0.485651 |  -0.286001 | -0.010133 | -0.100388 | -0.080038 | -0.062391 | -0.098954 | -0.274138 | -0.045576 | -0.381555 |  -0.157929 |        -0.00378 |  -0.061184 | -0.542983 | -0.00756 | -0.010692 | -0.027005 | -0.010692 | -0.020006 | -0.006547 | -0.022369 | -0.020006 | -0.031642 | -0.346897 | -0.223800 | -0.609654 |  1.029838 |  -0.00756 | -0.259771 |  -0.00378 |
|    2 | -0.137235 |  0.551559 | -0.069182 | -0.333087 | -0.353128 | -0.122447 | -0.111416 | -0.005500 |  -0.286001 | -0.010132 | -0.100388 | -0.080038 | -0.062391 | -0.098954 | -0.274138 | -0.045576 | -0.381555 |  -0.157929 |        -0.00378 |  -0.061184 | -0.542983 | -0.00756 | -0.010692 | -0.027005 | -0.010692 | -0.020006 | -0.006547 | -0.022369 | -0.020006 | -0.031642 | -0.346897 | -0.223800 | -0.609654 |  1.029838 |  -0.00756 | -0.259771 |  -0.00378 |
|    3 | -1.715936 |  1.779365 | -0.069182 | -0.333087 | -0.353128 |  0.503027 |  0.735918 | -0.490266 |   4.813713 | -0.010103 | -0.100388 | -0.080038 | -0.062391 | -0.098954 |  1.253659 |  0.131864 |  1.832953 |  -0.157929 |        -0.00378 |  -0.061184 |  1.841678 | -0.00756 | -0.010692 | -0.027005 | -0.010692 | -0.020006 | -0.006547 | -0.022369 | -0.020006 | -0.031642 |  2.882701 | -0.223800 | -0.609654 | -0.971027 |  -0.00756 | -0.259771 |  -0.00378 |
|    4 |  1.394112 | -0.808060 | -0.069182 | -0.333087 | -0.353128 | -0.122447 | -0.034386 | -0.637469 |   0.023486 | -0.010133 | -0.100388 | -0.080038 | -0.062391 | -0.098954 |  1.740533 |  0.053290 |  2.694088 |  -0.157929 |        -0.00378 |  -0.061184 |  1.841678 | -0.00756 | -0.010692 | -0.027005 | -0.010692 | -0.020006 | -0.006547 | -0.022369 | -0.020006 | -0.031642 | -0.346897 |  4.468282 | -0.609654 | -0.971027 |  -0.00756 | -0.259771 |  -0.00378 |



### 5.2.2   Binary Classification - Model Comparison Results

Following is the comparison between the 4 models:

```

                    Model     Train Accuracy     Test Accuracy
0     Logistic Regression           0.960319          0.962491
1                     KNN           1.000000          0.971827
2           Decision Tree           0.983725          0.972027
3                     SVC           0.982810          0.963758
```

```

```

 

|           | algorithm |                    params                         | mean_score | std_score |                      cv_result                    |
| --------: | --------: | ------------------------------------------------: | ---------: | --------: | ------------------------------------------------- |
|         0 |     LR    | {'C': 11.288378916846883, 'max_iter': 5000, 'm... |  0.960219  |  0.000787 | {'mean_fit_time': [0.006623983383178711, 0.005... |
|         1 |    KNN    | {'metric': 'manhattan', 'n_neighbors': 13, 'we... |  0.971822  |  0.000192 | {'mean_fit_time': [0.007259686787923177, 0.011... |
|         2 |     DT    | {'criterion': 'entropy', 'max_depth': 10, 'min... |  0.983110  |  0.000793 | {'mean_fit_time': [0.05327630043029785, 0.0530... |
|         3 |    SVC    |          {'C': 1000, 'gamma': 1, 'kernel': 'rbf'} |  0.978195  |  0.000647 | {'mean_fit_time': [1671.4753562609355, 1586.56... |



![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/confusion_matrix_binary.png) 

**Figure 16 - Binary Classification - Confusion Matrix**



Figure 16 provides the confusion matrix for the four models with the following additional information per model:

```
Model = LogisticRegression(C=11.288378916846883, max_iter=5000,
                   multi_class='multinomial', solver='sag') AUC = 0.99

Model = KNeighborsClassifier(metric='manhattan', n_neighbors=13, weights='distance') AUC = 1.0

Model = DecisionTreeClassifier(criterion='entropy', max_depth=10, min_samples_leaf=5) AUC = 1.0

Model = SVC(C=1000, gamma=1, probability=True) AUC = 0.98
```



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/test_best_model_binary_confusion_matrix.png) 

**Figure 17 - Best Model (DecisionTreeClassifier) Confusion Matrix with ROC Plot**



### 5.2.3   Feature engineering and exploration 

 Figure 18 provides the important features selected by the best model.

 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/bin_permutation_importance.png) 

**Figure 18 - Important features selected by the best model**

Base on the results presented in Figure 20, following are the important features identified by the model:

a) Offset  

b) sTtl

c) State_INT

d) Dur

e) sHops

f) Proto_icmp

g) TotPkts

h) State_RST

i) TcpRtt



These features are identified as important features based on binary classification algorithm and accordingly needs to be analyzed further. Using this results of the analysis, the data can be optimzed to improve the execution of the models.



Lets examine 'Offset', 'sTtl', 'Dur' from the important features selected by the model:



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/offset_density.png) 

**Figure 19 - Benign & Malicious 'Offset' Density**



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/sttl_density.png) 

**Figure 20 - Benign & Malicious 'sTtl' Density**



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/dur_density.png) 

**Figure 21 - Benign & Malicious 'Dur' Density**





### 5.3.   Multi-class Classification

### 5.3.1 Summary of Assessment Results 

The dataset was split as follows:

```
Xmc_train shape = (69983, 37)
 Xmc_test shape = (29993, 37)
ymc_train shape = (69983,)
 ymc_test shape = (29993,)
```

Following is a sample view of the normal data:

|      |   level_0 |       Dur |      sTos |      sTtl |     sHops |   TotPkts |   DstPkts |    Offset | dMeanPktSz |      Load |      Loss |   SrcLoss |   DstLoss |     pLoss |    TcpRtt |    SynAck |    AckDat | Proto_icmp | Proto_ipv6-icmp | Proto_sctp | Proto_tcp |   sDSb_4 |   sDSb_52 | sDSb_af11 | sDSb_af12 | sDSb_af41 |  sDSb_cs4 |  sDSb_cs6 |  sDSb_cs7 | State_ACC | State_CON | State_FIN | State_INT | State_REQ | State_RSP | State_RST | State_TST |
| ---: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | ---------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | ---------: | --------------: | ---------: | --------: | -------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: | --------: |
|    0 | -0.294618 |  0.720003 | -0.069182 | -0.333087 | -0.353128 | -0.122447 | -0.111416 |  0.693212 |  -0.286001 | -0.010133 | -0.100388 | -0.080038 | -0.062391 | -0.098954 | -0.274138 | -0.045576 | -0.381555 |  -0.157929 |        -0.00378 |  -0.061184 | -0.542983 | -0.00756 | -0.010692 | -0.027005 | -0.010692 | -0.020006 | -0.006547 | -0.022369 | -0.020006 | -0.031642 | -0.346897 | -0.223800 | -0.609654 |  1.029838 |  -0.00756 | -0.259771 |  -0.00378 |
|    1 |  0.829196 |  1.903937 | -0.069182 | -0.333087 | -0.353128 | -0.122447 | -0.111416 | -0.485651 |  -0.286001 | -0.010133 | -0.100388 | -0.080038 | -0.062391 | -0.098954 | -0.274138 | -0.045576 | -0.381555 |  -0.157929 |        -0.00378 |  -0.061184 | -0.542983 | -0.00756 | -0.010692 | -0.027005 | -0.010692 | -0.020006 | -0.006547 | -0.022369 | -0.020006 | -0.031642 | -0.346897 | -0.223800 | -0.609654 |  1.029838 |  -0.00756 | -0.259771 |  -0.00378 |
|    2 | -0.137235 |  0.551559 | -0.069182 | -0.333087 | -0.353128 | -0.122447 | -0.111416 | -0.005500 |  -0.286001 | -0.010132 | -0.100388 | -0.080038 | -0.062391 | -0.098954 | -0.274138 | -0.045576 | -0.381555 |  -0.157929 |        -0.00378 |  -0.061184 | -0.542983 | -0.00756 | -0.010692 | -0.027005 | -0.010692 | -0.020006 | -0.006547 | -0.022369 | -0.020006 | -0.031642 | -0.346897 | -0.223800 | -0.609654 |  1.029838 |  -0.00756 | -0.259771 |  -0.00378 |
|    3 | -1.715936 |  1.779365 | -0.069182 | -0.333087 | -0.353128 |  0.503027 |  0.735918 | -0.490266 |   4.813713 | -0.010103 | -0.100388 | -0.080038 | -0.062391 | -0.098954 |  1.253659 |  0.131864 |  1.832953 |  -0.157929 |        -0.00378 |  -0.061184 |  1.841678 | -0.00756 | -0.010692 | -0.027005 | -0.010692 | -0.020006 | -0.006547 | -0.022369 | -0.020006 | -0.031642 |  2.882701 | -0.223800 | -0.609654 | -0.971027 |  -0.00756 | -0.259771 |  -0.00378 |
|    4 |  1.394112 | -0.808060 | -0.069182 | -0.333087 | -0.353128 | -0.122447 | -0.034386 | -0.637469 |   0.023486 | -0.010133 | -0.100388 | -0.080038 | -0.062391 | -0.098954 |  1.740533 |  0.053290 |  2.694088 |  -0.157929 |        -0.00378 |  -0.061184 |  1.841678 | -0.00756 | -0.010692 | -0.027005 | -0.010692 | -0.020006 | -0.006547 | -0.022369 | -0.020006 | -0.031642 | -0.346897 |  4.468282 | -0.609654 | -0.971027 |  -0.00756 | -0.259771 |  -0.00378 |



### 5.3.2   Multi-class Classification Model Comparison

Following is the comparison between the 4 models:

```
                 Model  Train Accuracy  Test Accuracy
0  Logistic Regression        0.960790       0.941620
1                  KNN        1.000000       0.968193
2        Decision Tree        0.981095       0.951255
3                  SVC        0.981353       0.963758
```

|           |algorithm |                                            params | mean_score | std_score |                   cv_result                       |
| --------: | -------: | ------------------------------------------------: | ---------: | --------: | ------------------------------------------------- |
|         0 |     LR   | {'C': 545.5594781168514, 'max_iter': 100, 'mul... |  0.960162  |  0.000272 | {'mean_fit_time': [0.006397644678751628, 0.006... |
|         1 |    KNN   | {'metric': 'manhattan', 'n_neighbors': 13, 'we... |  0.968035  |  0.000519 | {'mean_fit_time': [0.007612864176432292, 0.010... |
|         2 |     DT   | {'criterion': 'gini', 'max_depth': 10, 'min_sa... |  0.979481  |  0.001875 | {'mean_fit_time': [0.0443574587504069, 0.04441... |
|         3 |    SVC   |          {'C': 1000, 'gamma': 1, 'kernel': 'rbf'} |  0.975551  |  0.001145 | {'mean_fit_time': [1149.4403246243794, 76.0082... |







![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/confusion_matrix_multi-class.png) 

**Figure 22 - Multi-class Classification - Confusion Matrix**



Figure 22 provides the confusion matrix for the four models with the following additional information per model:

```
Model = LogisticRegression(C=545.5594781168514, multi_class='multinomial',
                   solver='newton-cg') AUC = 1.0

Model = KNeighborsClassifier(metric='manhattan', n_neighbors=13, weights='distance') AUC = 1.0

Model = DecisionTreeClassifier(max_depth=10, min_samples_leaf=5) AUC = 1.0

Model = SVC(C=1000, gamma=1, probability=True) AUC = 1.0
```





 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/test_best_model_multi-class_confusion_matrix.png) 

**Figure 23 - Best Model (KNN) Confusion Matrix with ROC Plot**



### 5.3.3   Feature engineering and exploration 

 Figure 18 provides the important features selected by the best model.

 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/multi-class_permutation_importance.png) 

**Figure 24 - Important features selected by the best model**

Base on the results presented in Figure 24, following are the important features identified by the model:

a) Offset  

b) sTtl

c) sHops

d) State_INT

e) Proto_tco

f) Dur

etc ...



Lets examine 'Offset', 'sTls', and 'sHops':

 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/mc_offset_density.png) 

**Figure 25 - Benign & Malicious 'Offset' Density**



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/mc_sttl_density.png) 

**Figure 26 - Benign & Malicious 'sTtl' Density**



 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/mc_shops_density.png) 

**Figure 27 - Benign & Malicious 'sHops' Density**





### 5.3.4   Additional  Evaluation of Binary & Multi-class Classification Models



### 5.3.4.1   Binary Classification Model Evaluation - Target Feature 'Label'

```
LR
              precision    recall  f1-score   support

   Malicious       0.96      0.94      0.95     11827
      Benign       0.96      0.98      0.97     18166

    accuracy                           0.96     29993
   macro avg       0.96      0.96      0.96     29993
weighted avg       0.96      0.96      0.96     29993

KNN
              precision    recall  f1-score   support

   Malicious       0.98      0.95      0.96     11827
      Benign       0.97      0.99      0.98     18166

    accuracy                           0.97     29993
   macro avg       0.97      0.97      0.97     29993
weighted avg       0.97      0.97      0.97     29993

DT
              precision    recall  f1-score   support

   Malicious       0.99      0.94      0.96     11827
      Benign       0.96      1.00      0.98     18166

    accuracy                           0.97     29993
   macro avg       0.98      0.97      0.97     29993
weighted avg       0.97      0.97      0.97     29993

SVC
              precision    recall  f1-score   support

   Malicious       0.98      0.93      0.95     11827
      Benign       0.96      0.99      0.97     18166

    accuracy                           0.96     29993
   macro avg       0.97      0.96      0.96     29993
weighted avg       0.96      0.96      0.96     29993
```





### 5.3.4.2   Multi-class Classification Model Evaluation - Target Feature 'Attack Type'

```
LR
                precision    recall  f1-score   support

        Benign       0.97      0.90      0.93     11827
TCPConnectScan       0.92      1.00      0.95     11181
       SYNScan       0.97      0.86      0.91      3533
     HTTPFlood       0.88      0.97      0.92      1809
       UDPScan       0.95      0.99      0.97       476
     ICMPFlood       1.00      1.00      1.00       521
      UDPFlood       1.00      1.00      1.00       415
      SYNFlood       0.96      0.88      0.92       210
   SlowrateDoS       1.00      1.00      1.00        21

      accuracy                           0.94     29993
     macro avg       0.96      0.95      0.96     29993
  weighted avg       0.94      0.94      0.94     29993

KNN
                precision    recall  f1-score   support

        Benign       0.98      0.95      0.96     11827
TCPConnectScan       0.95      0.98      0.96     11181
       SYNScan       0.98      0.99      0.99      3533
     HTTPFlood       0.97      0.97      0.97      1809
       UDPScan       0.95      0.99      0.97       476
     ICMPFlood       1.00      1.00      1.00       521
      UDPFlood       1.00      1.00      1.00       415
      SYNFlood       0.96      0.88      0.92       210
   SlowrateDoS       0.95      1.00      0.98        21

      accuracy                           0.97     29993
     macro avg       0.97      0.97      0.97     29993
  weighted avg       0.97      0.97      0.97     29993

DT
                precision    recall  f1-score   support

        Benign       1.00      0.94      0.97     11827
TCPConnectScan       0.94      1.00      0.97     11181
       SYNScan       0.99      0.85      0.91      3533
     HTTPFlood       0.77      0.99      0.87      1809
       UDPScan       0.94      0.99      0.97       476
     ICMPFlood       1.00      1.00      1.00       521
      UDPFlood       1.00      1.00      1.00       415
      SYNFlood       1.00      0.88      0.93       210
   SlowrateDoS       1.00      1.00      1.00        21

      accuracy                           0.96     29993
     macro avg       0.96      0.96      0.96     29993
  weighted avg       0.96      0.96      0.96     29993

SVC
                precision    recall  f1-score   support

        Benign       0.98      0.93      0.96     11827
TCPConnectScan       0.93      1.00      0.96     11181
       SYNScan       0.99      0.96      0.97      3533
     HTTPFlood       0.99      0.98      0.98      1809
       UDPScan       0.95      0.99      0.97       476
     ICMPFlood       1.00      1.00      1.00       521
      UDPFlood       1.00      1.00      1.00       415
      SYNFlood       1.00      0.88      0.93       210
   SlowrateDoS       1.00      1.00      1.00        21

      accuracy                           0.96     29993
     macro avg       0.98      0.97      0.98     29993
  weighted avg       0.97      0.96      0.96     29993
```



Summarized per class:

```

'Model: LogisticRegression'
```

|      |        Classes | precision |   recall | f1-score | support |
| ---: | -------------: | --------: | -------: | -------: | ------: |
|    0 |         Benign |  0.966977 | 0.903695 | 0.934266 |   11827 |
|    1 |       UDPFlood |  0.916119 | 0.997317 | 0.954995 |   11181 |
|    2 |      HTTPFlood |  0.972133 | 0.859043 | 0.912096 |    3533 |
|    3 |    SlowrateDoS |  0.878939 | 0.971255 | 0.922794 |    1809 |
|    4 | TCPConnectScan |  0.945674 | 0.987395 | 0.966084 |     476 |
|    5 |        SYNScan |  0.998084 | 1.000000 | 0.999041 |     521 |
|    6 |        UDPScan |  0.997596 | 1.000000 | 0.998797 |     415 |
|    7 |       SYNFlood |  0.963351 | 0.876190 | 0.917706 |     210 |
|    8 |      ICMPFlood |  1.000000 | 1.000000 | 1.000000 |      21 |

```

'Model: KNeighborsClassifier'
```

|      |        Classes | precision |   recall | f1-score | support |
| ---: | -------------: | --------: | -------: | -------: | ------: |
|    0 |         Benign |  0.979067 | 0.949100 | 0.963850 |   11827 |
|    1 |       UDPFlood |  0.951239 | 0.978803 | 0.964824 |   11181 |
|    2 |      HTTPFlood |  0.982570 | 0.989244 | 0.985896 |    3533 |
|    3 |    SlowrateDoS |  0.969747 | 0.974572 | 0.972153 |    1809 |
|    4 | TCPConnectScan |  0.947791 | 0.991597 | 0.969199 |     476 |
|    5 |        SYNScan |  0.998081 | 0.998081 | 0.998081 |     521 |
|    6 |        UDPScan |  0.997596 | 1.000000 | 0.998797 |     415 |
|    7 |       SYNFlood |  0.963351 | 0.876190 | 0.917706 |     210 |
|    8 |      ICMPFlood |  0.954545 | 1.000000 | 0.976744 |      21 |

```

'Model: DecisionTreeClassifier'
```

|      |        Classes | precision |   recall | f1-score | support |
| ---: | -------------: | --------: | -------: | -------: | ------: |
|    0 |         Benign |  0.996949 | 0.939291 | 0.967262 |   11827 |
|    1 |       UDPFlood |  0.939723 | 0.996959 | 0.967496 |   11181 |
|    2 |      HTTPFlood |  0.988838 | 0.852533 | 0.915641 |    3533 |
|    3 |    SlowrateDoS |  0.732400 | 0.983416 | 0.839547 |    1809 |
|    4 | TCPConnectScan |  0.944112 | 0.993697 | 0.968270 |     476 |
|    5 |        SYNScan |  1.000000 | 0.996161 | 0.998077 |     521 |
|    6 |        UDPScan |  0.997596 | 1.000000 | 0.998797 |     415 |
|    7 |       SYNFlood |  1.000000 | 0.266667 | 0.421053 |     210 |
|    8 |      ICMPFlood |  1.000000 | 1.000000 | 1.000000 |      21 |

 ![AIML-Portfolio-Melicious-Attack-Classifiers/images/proto_benign_malicious.png at main · bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers](https://github.com/bhaswarey/AIML-Portfolio-Melicious-Attack-Classifiers/blob/main/images/test_best_model_multi-class_one_vs_one_matrix.png) 

**Figure 28 - Multi-class Classification - One-Vs-One Matrix**







### 6.0   Deployment



### 6.0.1   Summary

- For binary classification, target feature is balanced
- For multi-class classification, target feature is imbalanced. Therefore, examined F1-score.
- All of the models performed weel. The best model for binary classification is DT while the best model for multi-class classification is KNN.
- DT and KNN performance was very close, therefore for deployment, KNN will be used to predict 'Label' at level 1 and 'Attack Type' at level 2.



### 6.0.2   Recommendation

Further analysis needs to be conducted to improve the performance of the models in terms of execution time. In the case of multi-class classification where the target feature is 'Attack Type', a technique need to be formulated such that when the data is down sampled the result is a balanced data set.



### 7.0   Next Steps

To achieve practical implementation, the code and algorithm must be optimized to process large amounts of data (in Megabytes) in very short period of time (in minutes). Further analysis is required to reduce the number of input features evident from results in section 5.3.3 and 5.2.3.
