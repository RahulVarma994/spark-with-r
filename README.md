# spark-with-r
install sparklyr package 
# Load sparklyr
library(sparklyr)
# Connect to your Spark cluster
spark_conn = spark_connect(master = "local")
# Print the version of Spark
spark_version(sc = spark_conn)
#Explore track_metadata structure
str(track_metadata)
# Copy track_metadata to Spark
track_metadata_tbl <- copy_to(spark_conn, track_metadata)


# Disconnect from Spark
spark_disconnect(sc = spark_conn)
