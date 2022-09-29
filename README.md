# Step by step guide to creating an Azure stream analytics pipeline with Azure Events Hub

## Step 1: Create an Azure Events Hub Namespace and an Event Hub


### Go to Azure home page -> search for the Events Hub resource -> go to the Events Hub page -> Create new Namespace -> give it a name, choose resource group, subscription, throughput units, pricing tier, then review and create

#### The throughput capacity of Event Hubs is controlled by throughput units. Throughput units are pre-purchased units of capacity. A single throughput unit lets you:

    Ingress: Up to 1 MB per second or 1000 events per second (whichever comes first).
    Egress: Up to 2 MB per second or 4096 events per second.
#### so choose the throughput unit and pricing tier (descriptions found while creating the namespace) according to your use case

### Now go to the resource -> Entities -> Event Hub -> Create new -> Give it a name -> choose partition count (min. 2) ->create

#### Partitions help parallelize the streaming job into the event hub

## Step 2: Configure your Event Hub

### Go to your event hub resource -> shared access policy -> add -> choose Manage -> give a name -> A primary key and a connection string will be created which will be used later in the python script to connect to the event hub

## Step3:  Create an Azure Stream Analytics job

### Create an azure stream analytics job from its resource page -> give it a name -> choose resource group and subscription as before -> choose location(same as Event Hub namespace) -> choose no. of streaming units (the more the streaming units, the faster the data is analyzed) -> create

## Step 4: Configure the stream analytics job

### Go to the resource page for the job -> Inputs -> add stream input -> Event Hub -> on the new input configure window, choose the event hub namespace and event hub that is already created and for authentication mode, use connection string -> give it a name and save

### Go to Outputs from the stream analytics resource page -> add -> select ADLS gen 2 storage -> configure it (create a new container, use connection string for authentication) -> create it

### Now go to the query tab from the stream analytics resource page, choose the input and output resources that we just created in i/p and o/p's place, then save the query

## Step 5: Configure the python script

### From the event hub page, go to shared policies, copy the connection string and pass its value to the 'connection_str' variable on the python script and pass the eventhub name to the 'eventhub_name' variable

## Step 6: Run the script and the query

### Run your python script and then run your query from the stream analytics page, check if data is being pulled correctly by the pipeline. Check if input is receiving data from the source and whether the output is receiving that data. If everything looks good, proceed

## Step 7: Run the job

### Go to Overview of the stream analytics job page -> Start. Don't forget to stop the job once it's done
