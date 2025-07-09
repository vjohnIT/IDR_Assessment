## IDR_ADF_Databricks


## Guest: Overview

A csv file is been provided containing the guest information with their contacts. The data needs to processed using data pipeline tools and objective is to provide useful data to the sales and marketing team.
Possible analytics information :  How many guest are in which state : traveled,paid in full, depoist etc ? Can the guest be contacted through phones and emails 

### Design 

![image](https://github.com/user-attachments/assets/b5672e41-bf50-47bb-b735-ae0061e6aa09)




### Approach

- Build a data pipeline using medallion data layers .
- Staging layer will have the files placed. Use ADF to browse the folder and copy the data to the Bronze layer as a parquet files,  include the current date as derived column
- In the Bronze layer,  select the desired columns.For unique columns selected combination of  guest number and the guest name as business key column. Created a hash value and included in the data
- In the Silver layer (append) -  data is merged with existing records , existing  records ( phone, email , address , state)  are updated using the hash value and new records are inserted 
- Further the data is refined by validating ,two attritutes realted to contacts - email and phone.  If the values are as per the data specification the rows are marked good
- In the Gold layer (overwrite) -  data is selected that are valid from the silver layer 



### ADF Snapshot


![image](https://github.com/user-attachments/assets/dc79d27e-ec67-48d5-aa68-3cf1958d2fd4)



### General analytics features

| Analytic                     |    Counts    |
| ---------------------------- | -----------  |
| Number of  records           |  100,000     |
| Number of unique Guest names |  35          |
| Number of unique Guest num   |  92,543      |
| Number of unique phone num   |  99,999      |



| State       |        Guest Count         |
|-------------|----------------------------   |
|booked not departed |      12,668|
| paid partial |      12,600|
|canceled |      12,419|
| inquiring|      12,598|
|deposit |      12,583|
|  pending|      12,423|
| traveled|      12,438|
|paid in full|      12,271|






