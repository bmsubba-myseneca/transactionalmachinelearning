# transactional machine learning
Transactional Machine Learning (TML) using Data Streams and AutoML

**Fast data requires fast machine learning**  

Apply auto machine learning to data streams and create transactional machine learning (TML) solutions that are:
 
 **frictionless**: require minimal to no human intervention 
 
 **elastic**: machine learning solutions that can scale up or down by controlling the number of data streams, algorithms, and users of the insights
  
 Strengthen your knowledge of the inner workings of TML solutions using data streams with auto machine learning integrated with Apache Kafka.  You will be at the forefront of an exciting area of machine learning that is focused on speed of data and algorithm creation, scale, and automation.

**Create Your First TML Solution with Kafka by Downloading:**

1) MAADS-VIPER: https://www.confluent.io/hub/oticsinc/maads-viper (Official Kafka connector for TML - Linux version).  **Latest** Linux/Windows version can be found here: https://github.com/smaurice101/maads-viper)
2) MAADS-HPDE: https://github.com/smaurice101/MAADS-HPDE (Windows/Linux versions available)
3) MAADS-Python Library: https://pypi.org/project/maads/
4) Create a Kafka Cluster at Confluent Cloud: https://www.confluent.io/confluent-cloud

**For Advanced users who want to integrate TML with MAADS DEEP LEARNING technology should email info@otics.ca**

**Contact**: 

For any help and additional information, or if your token has expired you can e-mail: info@otics.ca or goto http://www.otics.ca, and we would be happy to help you! OTICS will provide 1 hour free developer session on TML if needed.

**Read Medium blog**: https://sebastian-maurice.medium.com/transactional-machine-learning-with-data-streams-for-real-time-predictions-and-optimization-using-eb12c4df597c

**Read Confluent blog**: Link coming soon.

**EXAMPLE TML PYTHON CODE**
```python
import maads
#If using Jupyer Notebook then use this library
import nest_asyncio
import json

#If using Jupyer Notebook then use this command
nest_asyncio.apply()

#jupyter notebook --NotebookApp.iopub_data_rate_limit=1.0e10

```


```python
#Join streams of data
# Stream 1: Dependentvariable
# Stream 2: Independentvariable1
# Stream 3: Independentvariable2

VIPERHOST="http://192.168.0.13"
VIPERPORT=8000
hpdehost="http://192.168.0.13"
hpdeport=8001
viperconfigfile="viper.env"

def getparams():
        
     with open("admin.tok", "r") as f:
        VIPERTOKEN=f.read()
  
     return VIPERTOKEN
#############################################################################################################
#                                           GET VIPER TOKEN
VIPERTOKEN=getparams()
#############################################################################################################

#############################################################################################################
#                                     CREATE TOPICS IN KAFKA
# First Create a topic to produce to

producetotopic="viperdependentvariable"
result3=maads.vipercreatetopic(VIPERTOKEN,VIPERHOST,VIPERPORT,producetotopic,"OTICS","Sebastian",
                           #    "Sebastian.maurice","Toronto", "Test Training",enabletls=1,
                            #   brokerhost='',brokerport=-999,numpartitions=3,replication=3,microserviceid='')
y = json.loads(result3)
producetotopic=y['Topic']
producerid=y['ProducerId']
print(producerid)


# First Create a topic to produce to
producetotopic="viperindependentvariable1"
result3=maads.vipercreatetopic(VIPERTOKEN,VIPERHOST,VIPERPORT,producetotopic,"OTICS","Sebastian",
                             #  "Sebastian.maurice","Toronto", "Test Training",enabletls=1,
                              # brokerhost='',brokerport=-999,numpartitions=3,replication=3,microserviceid='')
y = json.loads(result3)
producetotopic=y['Topic']
producerid=y['ProducerId']
print(producerid)


# First Create a topic to produce to
producetotopic="viperindependentvariable2"
result3=maads.vipercreatetopic(VIPERTOKEN,VIPERHOST,VIPERPORT,producetotopic,"OTICS","Sebastian",
                            #   "Sebastian.maurice","Toronto", "Test Training",enabletls=1,
                             #  brokerhost='',brokerport=-999,numpartitions=3,replication=3,microserviceid='')
y = json.loads(result3)
producetotopic=y['Topic']
producerid=y['ProducerId']
print(producerid)

#############################################################################################################
#                                     PRODUCE External Value to TOPIC STREAMS
# produce to Topic

topics=["viperdependentvariable","viperindependentvariable1","viperindependentvariable2"]
producerids=["ProducerId-vTXnd4FJqfmBahbLPMjjFxIrvUqR11","ProducerId-iq2YUiU6IbIzAOsAlTI95njaaHyWgk",
             "ProducerId-GEjx2o7jkfA4aezkEnGCowGlt2yTv0"]

for j in range(500):  
    for t,p in zip(topics,producerids):
      num=str(random.randrange(1000)) 
      result=maads.viperproducetotopic(VIPERTOKEN,VIPERHOST,VIPERPORT,t,p,1,1000,'','', '',0,num)
      
#############################################################################################################
#                                     JOIN DATA STREAMS 
# "viperdependentvariable,viperindependentvariable1,viperindependentvariable2"

joinedtopic="joined-viper-test11"
result=maads.vipercreatejointopicstreams(VIPERTOKEN,VIPERHOST,VIPERPORT,"joined-viper-test11",
                    "viperdependentvariable,viperindependentvariable1,viperindependentvariable2",
                   "OTICS","Sebastian","Sebastian.Maurice", "Test","Toronto",
                   enabletls=1,brokerhost="",brokerport=-999,replication=3,numpartitions=3,microserviceid='')

print(result)
y = json.loads(result)
topic=y['Topic']
producerid=y['ProducerId']


#############################################################################################################

#############################################################################################################
#                                     SUBSCRIBE TO STREAM TOPIC

#result3=maads.vipersubscribeconsumer(VIPERTOKEN,VIPERHOST,VIPERPORT,topic,"OTICS","Sebastian","Sebastian.Maurice@otics.ca"
                                   #  "Toronto","Test","Test",brokerhost='',brokerport=-999,groupid='',microserviceid='')
#print(result3)
#y = json.loads(result3)
consumerid="ConsumerId-Gu-TPSextT6NHj6ZzPG03iTqs21Wwt"

```

    {"WARN":"Topic already exists","ProducerId":"ProducerId-HD9XNXWwX6fchOtKjcPOwSWZczPaGM","Topic":"joined-viper-test11"}
    


```python
#############################################################################################################
#                                      PRODUCE DATA TO STREAM: joined-viper-test11

#result2=maads.viperproducetotopicstream(VIPERTOKEN,VIPERHOST,VIPERPORT,topic,producerid,-1,50,1,10000, '',-999,'')
#print(topic)
#print(result2)



```


```python
#############################################################################################################
#                           CREATE TOPIC TO SAVE TRAINING DATA SET FROM STREAM

# Frist Create a topic to produce to
producetotopic="trainingdata2"
result3=maads.vipercreatetopic(VIPERTOKEN,VIPERHOST,VIPERPORT,producetotopic,"OTICS","Sebastian",
                               "Sebastian.maurice","Toronto", "Test Training",enabletls=1,
                               brokerhost='',brokerport=-999,numpartitions=3,replication=3,microserviceid='')
y = json.loads(result3)
producetotopic=y['Topic']
producerid=y['ProducerId']

#############################################################################################################
#                           CREATE TRAINING DATA SET FROM JOINED STREAM TOPIC

consumefrom=topic
#print(topic)
#result=maads.viperconsumefromtopic(VIPERTOKEN,VIPERHOST,VIPERPORT,topic,consumerid,"OTICS",-1,1,10000,-1)
    
#print(result)
result4=maads.vipercreatetrainingdata(VIPERTOKEN,VIPERHOST,VIPERPORT,consumefrom,producetotopic,"viperdependentvariable", 
                             "viperindependentvariable1,viperindependentvariable2",consumerid,producerid,
                             "OTICS",-1,1,60000, '',-999,'')

#print(result4)
#return


```


```python
#############################################################################################################
#                         SUBSCRIBE TO TRAINING DATA TOPIC  

producetotopic="trainingdata2"
result=maads.vipersubscribeconsumer(VIPERTOKEN,VIPERHOST,VIPERPORT,producetotopic,"OTICS","Sebastian","Sebastian.Maurice"
                                     "Toronto","Test","Test",brokerhost='',brokerport=-999,groupid='',microserviceid='')
#print(result)
y = json.loads(result)
consumeridtrainingdata2=y['Consumerid']

#############################################################################################################
#                         CREATE TOPIC TO STORE TRAINED PARAMS FROM ALGORITHM  
# Frist Create a topic to produce to

consumefrom=producetotopic
producetotopic="trainined-params"
result5=maads.vipercreatetopic(VIPERTOKEN,VIPERHOST,VIPERPORT,producetotopic,"OTICS","Sebastian",
                               "Sebastian.maurice","Toronto", "Test Training",enabletls=1,
                               brokerhost='',brokerport=-999,numpartitions=3,replication=3,microserviceid='')
print(result5)
y = json.loads(result5)
producetotopic=y['Topic']
producerid=y['ProducerId']

#############################################################################################################
#                         VIPER CALLS HPDE TO PERFORM REAL_TIME MACHINE LEARNING ON TRAINING DATA 


consumefrom="trainingdata2"
producetotopic="trainined-params"
result6=maads.viperhpdetraining(VIPERTOKEN,VIPERHOST,VIPERPORT,consumefrom,producetotopic,"OTICS",consumeridtrainingdata2,
                        producerid, hpdehost,viperconfigfile,1,-1,10,hpdeport,-1,0,'',-999,280,'')    
print(result6)
y = json.loads(result6)
algokey=y['Algokey']


#############################################################################################################
#                                     SUBSCRIBE TO STREAM TOPIC

producetotopic="trainined-params"
result=maads.vipersubscribeconsumer(VIPERTOKEN,VIPERHOST,VIPERPORT,producetotopic,"OTICS","Sebastian","Sebastian.Maurice"
                                     "Toronto","Test","Test",brokerhost='',brokerport=-999,groupid='',microserviceid='')
print(result)
y = json.loads(result)
consumeridtraininedparams=y['Consumerid']
print(consumeridtraininedparams)
consumefrom=producetotopic


#############################################################################################################
#                         CREATE TOPIC TO STORE PREDICTIONS FROM ALGORITHM  
# Frist Create a topic to produce to

producetotopic="hyper-predictions"
result=maads.vipercreatetopic(VIPERTOKEN,VIPERHOST,VIPERPORT,producetotopic,"OTICS","Sebastian",
                               "Sebastian.maurice","Toronto", "Test Training",enabletls=1,
                               brokerhost='',brokerport=-999,numpartitions=3,replication=3,microserviceid='')
print(result)
y = json.loads(result)
produceridhyperprediction=y['ProducerId']
print(produceridhyperprediction)

#############################################################################################################
#                                     SUBSCRIBE TO STREAM PREDICTION TOPIC

result=maads.vipersubscribeconsumer(VIPERTOKEN,VIPERHOST,VIPERPORT,producetotopic,"OTICS","Sebastian","Sebastian.Maurice",
                                     "Toronto","Test","Test",brokerhost='',brokerport=-999,groupid='',microserviceid='')
print(result)
y = json.loads(result)
streamconsumerid=y['Consumerid']
consumefrom=producetotopic


#############################################################################################################
#                                     START HYPER-PREDICTIONS FROM ESTIMATED PARAMETERS
producetotopic="hyper-predictions"        

#get data stream to predict
#resultsp=maads.viperconsumefromstreamtopic(VIPERTOKEN,VIPERHOST,VIPERPORT,"joined-viper-test11","ConsumerId-Gu-TPSextT6NHj6ZzPG03iTqs21Wwt",
                              #    "OTICS",-1, 1,10000,-1,'',-999,'')
#print(resultsp)                                
#inputdata="23,34"
inputdata="joined-viper-test11"


consumefrom="trainined-params"
result6=maads.viperhpdepredict(VIPERTOKEN,VIPERHOST,VIPERPORT,consumefrom,producetotopic,"OTICS",consumeridtraininedparams,
                                produceridhyperprediction, hpdehost,inputdata,'',-1,-1,1,
                                1000,hpdeport,'', -999,120,1,'')
print(result6)

#############################################################################################################
#                                     CREATE CONSUMER GROUP

topictoconsumefrom="hyper-predictions"
groupname="hyperprediction-group2"
result=maads.vipercreateconsumergroup(VIPERTOKEN,VIPERHOST,VIPERPORT,topictoconsumefrom,groupname,
                                      "OTICS","Sebastian","sebastian.maurice", "test","Toronto",1) 
    
print(result)        
print(result)
y = json.loads(result)
groupid=y['Groupid']

result=maads.viperconsumergroupconsumefromtopic(VIPERTOKEN,VIPERHOST,VIPERPORT,topictoconsumefrom,streamconsumerid,
                                                groupid,"OTICS",-1,1,1000,-1)

print(result)

#############################################################################################################
#                         CREATE TOPIC TO STORE OPTIMAL PARAMETERS FROM ALGORITHM  
# Frist Create a topic to produce to

producetotopic="hpde-optimal-parameters"
result=maads.vipercreatetopic(VIPERTOKEN,VIPERHOST,VIPERPORT,producetotopic,"OTICS","Sebastian",
                               "Sebastian.maurice","Toronto", "Test Training",enabletls=1,
                               brokerhost='',brokerport=-999,numpartitions=3,replication=3,microserviceid='')
print(result)
y = json.loads(result)
producerid=y['ProducerId']
#############################################################################################################
#                                     START MATHEMATICAL OPTIMIZATION FROM ALGORITHM
consumefrom="trainined-params"

result7=maads.viperhpdeoptimize(VIPERTOKEN,VIPERHOST,VIPERPORT,consumefrom,producetotopic,"OTICS",consumeridtraininedparams,
                                producerid,hpdehost,-1,-1,1,1000,hpdeport)
print(result7)

```

    {"Topic":"trainined-params","ProducerId":"ProducerId-fuj1ygdy-E5noyO2CtKjDN0S6UeaB4"}
    {
     "Algokey": "ConsumerId-IbBdZx3N7ZLgMJk7Sty42EINqatt2a_json",
     "Algo": "ConsumerId-IbBdZx3N7ZLgMJk7Sty42EINqatt2a_jsonrdg",
     "DependentVariable": "viperdependentvariable",
     "Forecastaccuracy": 0.001,
     "Filename": "./hpdedata/ConsumerId-IbBdZx3N7ZLgMJk7Sty42EINqatt2a.csv",
     "Fieldnames": "Date,viperindependentvariable1,viperindependentvariable2",
     "TestResultsFile": "./models/ConsumerId-IbBdZx3N7ZLgMJk7Sty42EINqatt2a_json_predictions.csv",
     "Deployed": 1,
     "DeployedTo": "Local Machine Deploy Folder",
     "Created": "2020-12-10T22:43:54.1909495-05:00"
    ,"ConsumeridFrom":"ConsumerId-IbBdZx3N7ZLgMJk7Sty42EINqatt2a","Producerid":"ProducerId-fuj1ygdy-E5noyO2CtKjDN0S6UeaB4","ConsumingFrom":"trainingdata2","ProduceTo":"trainined-params","Companyname":"OTICS","BrokerhostPort":"pkc-lgwgm.eastus2.azure.confluent.cloud:9092","Islogistic":0,"HPDEHOST":"192.168.0.13:8001","HPDEMACHINENAME":"Guru","Modelruns":10,"BytesWritten":908,"kafkakey":"1BwUtmRahTPuUYq24XmgLZ2BojZK01","Partition":1,"Offset":3}
    {"Consumerid":"ConsumerId-7cUROb7RjfugYKLk2YiS40b5AQ3KgB","Topic":"trainined-params"}
    ConsumerId-7cUROb7RjfugYKLk2YiS40b5AQ3KgB
    {"Topic":"hyper-predictions","ProducerId":"ProducerId-HWWwbtbXSykcitWtfN3vY3epHv5OLD"}
    ProducerId-HWWwbtbXSykcitWtfN3vY3epHv5OLD
    {"Consumerid":"ConsumerId-Kyr5jerKqh92XgtTkp6cb9asJpeZRY","Topic":"hyper-predictions"}
    {
     "Hyperprediction": 43.915,
     "Algokey": "ConsumerId-vYvc5Sc0QWPF-jpDzjGAaujhz75C9B_json",
     "Algo": "ConsumerId-vYvc5Sc0QWPF-jpDzjGAaujhz75C9B_jsongp",
     "Usedeploy": 1,
     "Created": "2020-12-10T22:44:24.267933-05:00"
    ,"ConsumeridHPDE":"ConsumerId-7cUROb7RjfugYKLk2YiS40b5AQ3KgB","Producerid":"ProducerId-HWWwbtbXSykcitWtfN3vY3epHv5OLD","HPDEHOST":"http://192.168.0.13","HPDEPORT":8001,"Consumefrom":"trainined-params","Produceto":"hyper-predictions","Brokerhost":"pkc-lgwgm.eastus2.azure.confluent.cloud","Brokerport":9092,"kafkakey":"qkmYvNt8ih3-Dnjw5lgrVj0lmx6hzE","Inputdata":"417,581","Partition":2,"Offset":21}{
     "Hyperprediction": 43.915,
     "Algokey": "ConsumerId-vYvc5Sc0QWPF-jpDzjGAaujhz75C9B_json",
     "Algo": "ConsumerId-vYvc5Sc0QWPF-jpDzjGAaujhz75C9B_jsongp",
     "Usedeploy": 1,
     "Created": "2020-12-10T22:44:24.7871717-05:00"
    ,"ConsumeridHPDE":"ConsumerId-7cUROb7RjfugYKLk2YiS40b5AQ3KgB","Producerid":"ProducerId-HWWwbtbXSykcitWtfN3vY3epHv5OLD","HPDEHOST":"http://192.168.0.13","HPDEPORT":8001,"Consumefrom":"trainined-params","Produceto":"hyper-predictions","Brokerhost":"pkc-lgwgm.eastus2.azure.confluent.cloud","Brokerport":9092,"kafkakey":"-BT6mMEgD36f3QvA0Hs0IlrK0D8wyK","Inputdata":"207,673","Partition":1,"Offset":24}{
     "Hyperprediction": 43.915,
     "Algokey": "ConsumerId-vYvc5Sc0QWPF-jpDzjGAaujhz75C9B_json",
     "Algo": "ConsumerId-vYvc5Sc0QWPF-jpDzjGAaujhz75C9B_jsongp",
     "Usedeploy": 1,
     "Created": "2020-12-10T22:44:25.3370807-05:00"
    ,"ConsumeridHPDE":"ConsumerId-7cUROb7RjfugYKLk2YiS40b5AQ3KgB","Producerid":"ProducerId-HWWwbtbXSykcitWtfN3vY3epHv5OLD","HPDEHOST":"http://192.168.0.13","HPDEPORT":8001,"Consumefrom":"trainined-params","Produceto":"hyper-predictions","Brokerhost":"pkc-lgwgm.eastus2.azure.confluent.cloud","Brokerport":9092,"kafkakey":"LGSllLWESdb1plUsX2Qug0CgHyvPak","Inputdata":"283,591","Partition":1,"Offset":25}
    {"Status":"Group name already exists","Groupid":"GroupId-hyperprediction-group2","Groupname":"hyperprediction-group2"}
    {"Status":"Group name already exists","Groupid":"GroupId-hyperprediction-group2","Groupname":"hyperprediction-group2"}
    {"LastOffset":0,"BytesRead":88,"Groupid":"GroupId-hyperprediction-group2","TopicReads":[]}
    {"Topic":"hpde-optimal-parameters","ProducerId":"ProducerId-xTo2TFMGy3-HPaVEkBFE581tbwkxU1"}
    {"UserDetails":{"CreatedOn":"Thu, 10 Dec 2020 22:44:41 EST","HPDEHOST":"192.168.0.13:8001","ConstraintType":"USE min/max for bounds","Epsilon":20,"StretchBounds":10,"Usedeploy":0},"OptimizedValues":{"Objective":"Maximization","ObjectiveFunctionValue":43.915,"OptimalValues":[{"viperindependentvariable1":819.136},{"viperindependentvariable2":948.618}]},"Constraints":[{"Max":863.45,"Min":575.634,"Variable":"viperindependentvariable1"},{"Max":1059.504,"Min":706.336,"Variable":"viperindependentvariable2"}],"DescriptiveStats":[{"Max":984,"Mean":497.719,"Min":10,"STD":269.092,"Variable":"viperindependentvariable1"},{"Max":995,"Mean":519.207,"Min":10,"STD":290.64,"Variable":"viperindependentvariable2"}],"AdditionDetails":{"Consumerid":"ConsumerId-7cUROb7RjfugYKLk2YiS40b5AQ3KgB","Producerid":"ProducerId-xTo2TFMGy3-HPaVEkBFE581tbwkxU1","Consumefrom":"trainined-params","Produceto":"hpde-optimal-parameters","Brokerhost":"pkc-lgwgm.eastus2.azure.confluent.cloud","Brokerport":9092,"BytesWritten":981,"kafkakey":"HBr8XLSGi98hKelzcMguMMzt12QqZP","Partition":2,"Offset":4}}
    


