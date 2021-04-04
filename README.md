# Assignment-_1
My first repository on GitHub
from pyspark.sql import SparkSession


spark = SparkSession.builder.appName('Assign_test').getOrCreate()

df_parquet = spark.read.parquet('C:/Users/Ankita/Downloads/consumerInternet.parquet')
df_csv = spark.read.option("header",True).csv('C:/Users/Ankita/Downloads/startup.csv')
df_final = df_csv.union(df_parquet)
df_final.head(2)

# How many startups are there in Pune City?
df_final.filter(df_final.City == 'Pune').count()

# Output : 105

# How many startups in Pune got their Seed/ Angel Funding?
df_final.filter(df_final.City == 'Pune').filter(df_final.InvestmentnType.rlike('(?=.*\ Angel\ Funding)')).count()
# Output : 5
